# Integrating Multiple REST Endpoints into 8base GraphQL

**Goal:** 

Build an application where when a User signs up, we populate their profile with enriched data (fake data), create's a "Welcome" Post to greet them, as well as return an awesome gif from Giphy to say "hi" when they view their profile page.

What we'll be using:

- For the Gif: [https://developers.giphy.com/explorer](https://developers.giphy.com/explorer)
- For the "Data Enrichment": [https://randomuser.me/api/?](https://randomuser.me/api/?exc=login)nat=GB
- For the GraphQL Backend: https://app.8base.com
- For the Frontend Application: [https://github.com/8base/vue-8base-starter-app](https://github.com/8base/vue-8base-starter-app)

Resources:

- GIPHY_API_TOKEN: avEEsnqJcAKBHW6oOYt5755odWmkqIxT

Step 1: Getting Set Up

Create an account at 8base.com. **Send Evgeny his email address as soon as he signs up to unlock the throttling.**

Once signed in, talk a little bit about Dashboard and Data Builder. Move over to the data builder then and create the *Posts* table accordingly.

**Posts**

title=Text - mandatory

body=Text - max 500

attachment=File - Image

User=Table - Posts

**Users (ADD FIELDS)**

gender=Text

birthday=Date - DateTime

cellPhone=Text

Explain then about how 8base is relational, so let's relate this with the User's table. 

Now hop into Settings → Environment Variables and add the GIPHY_API_TOKEN.

Create a new role called AppUser - Anyone using our app. Only read/update their own posts.

Set up an Authentication Profile called "Default Auth":

- 8base Auth
- Self Signup - on
- Roles - AppUser

Say that we'll save these keys for later. However, at this part we're already ready to jump to the CLI - but let's first explore the API Explorer.

```tsx
// Example

query {
  usersList {
    items {
      posts(filter: {
        title: {
          contains: "Welcome"
        }
      }) {
      	items {
          title
          body
        }
      }
    }
  }
}
```

Step 2: Building the Custom resolvers

Open the a terminal session and start by running:

```powershell
# Install the CLI
npm install 8base-cli -g

# Login to the CLI
8base login

# Create project with --empty flag
8base init jason-app --empty

# Move into dir
cd jason-app
```

We're then going to create a new 8base project once this is installed using the init command. If we use it without any flags, we'll get more templates than we need. So for now, lets just run it with the empty flag.

Once the project is set up talk a little about the types of functions we offer [webhook, task, trigger, resolver] and explain that for this project we're going to need/want three functions.

- randomUserEnrich - resolver: For "enriching" the user data that we care about.
- giphySearch - resolver: For finding some awesome gifs
- enrichAndWelcome - trigger: For enriching the data on signup.

So we can get started by generating these functions now, and the building them out as we go forward.

```bash
# Resolvers
8base g resolver randomUserEnrich
8base g resolver giphySearch

# Trigger
8base g trigger enrichAndWelcome --type=after --operation=User.create

# Open project in editor
code .
```

Now let's open it in a preferred editor.

**GiphySearch**

1. Go ahead and change return type in the handler.ts file to any (delete the return type)
2. Explain the context and event argument. 
3. Go to [https://developers.giphy.com/explorer](https://developers.giphy.com/explorer) use Search, Limit 1, request= "Excited"
4. Talk about getting all these arguments from our request, which we will do in the request.json file.
5. Go to the schema.graphql file now and explain how the two connect (request to schema).
6. Talk about typing out the JSON response in the Giphy API explorer, though how much easier it is to be copied over from what I have....
7. Now write the actual function, and talk about the transform of the keys.
    1. Make sure to `npm install axios @types/node -s` to make the requests.
8. When appropriate, suggest the transform key function.
9. Let's test it locally.
    1. `GIPHY_API_TOKEN=avEEsnqJcAKBHW6oOYt5755odWmkqIxT 8base invoke-local giphySearch -m request`

```tsx
// transformKey.js
export default function transformKey (obj, path, newKey) {
    if (path.length === 1) {
        obj[newKey] = obj[path]
        delete obj[path];
        return
    }
    return transformKey(obj[path[0]], path.slice(1), newKey)
}
```

```tsx
// schema.json

type GiphyImageOriginal {
  size: Int,
  width: Int,
  frames: Int,
  height: Int,
  mp4: String,
  url: String,
  webp: String,
  hash: String,
  mp4_size: Int,
  webp_size: Int
}

type GiphyImageSized {
    width: Int,
    height: Int,
    url: String,
    size: String
}

type GiphyImageWebp {
    url: String,
    width: Int,
    height: Int,
    size: String,
    webp: String,
    webp_size: Int,
}

type GiphyImageMp4 {
    width: Int,
    height: Int,
    mp4: String,
    mp4_size: Int,
}

type GiphyImageWebpMp4 {
    url: String,
    width: Int,
    height: Int,
    mp4: String,
    size: String,
    webp: String,
    mp4_size: Int,
    webp_size: Int,
}

type GiphyImageStill {
    url: String,
    width: Int,
    height: Int
}

type GiphyImageLooping {
    mp4: String,
    mp4_size: Int
}

type GiphyImageFormats {
  original: GiphyImageOriginal,
  downsized_large: GiphyImageSized,
  fixed_height_downsampled: GiphyImageWebp,
  fixed_height_small_still: GiphyImageSized,
  downsized_still: GiphyImageSized,
  fixed_height_still: GiphyImageSized,
  downsized_medium: GiphyImageSized,
  downsized: GiphyImageSized,
  preview_webp: GiphyImageSized,
  original_mp4: GiphyImageMp4,
  fixed_height_small: GiphyImageWebpMp4,
  fixed_height: GiphyImageWebpMp4,
  downsized_small: GiphyImageMp4,
  preview: GiphyImageMp4,
  fixed_width_downsampled: GiphyImageWebp,
  fixed_width_small_still: GiphyImageSized,
  fixed_width_small: GiphyImageWebpMp4,
  original_still: GiphyImageSized,
  fixed_width_still: GiphyImageSized,
  looping: GiphyImageLooping,
  fixed_width: GiphyImageWebpMp4,
  preview_gif: GiphyImageSized,
  four80_w_still: GiphyImageStill,
}

type GiphySearchResult {
  id: String,
  url: String,
  type: String,
  slug: String,
  title: String,
  source: String,
  rating: String,
  is_sticker: Int,
  username: String,
  embed_url: String,
  bitly_url: String,
  source_tld: String,
  content_url: String,
  bitly_gif_url: String,
  import_datetime: String,
  source_post_url: String,
  trending_datetime: String,
  images: GiphyImageFormats,
  analytics: GiphyAnalytics
}

type GiphyAnalyticsObject {
  url: String
}

type GiphyAnalytics {
    onsent: GiphyAnalyticsObject,
    onload: GiphyAnalyticsObject,
    onclick: GiphyAnalyticsObject
}

type GiphyPagination {
    total_count: Int, 
    offset: Int,
    count: Int 
}

type GiphyResult {
  count: Int,
  pagination: GiphyPagination,
  results: [GiphySearchResult!]
}

extend type Query {
  giphySearch(
    q: String!,
    limit: Int,
    offset: Int,
    lang: String,
    rating: String,
  ): GiphyResult
}
```

```json
// Request.json

{
  "data": {
    "q": "excited",
    "limit": "1",
    "offset": "0",
    "rating": "G",
    "lang": "en",
    "foo": "bar"
  },
  "headers": {
    "x-header-1": "header value"
  }
}
```

```jsx
// Handler.ts

import axios from 'axios';
import transformKey from '../transformKey';

export default async (event: any, ctx: any) : Promise<any> => {
  const { 
    search, 
    limit,
    lang = 'en',
    offset = 20,
    rating = 'G',
  } = event.data;

  let resp;

  try {
    resp = await axios.get([
      'https://api.giphy.com/v1/gifs/search?',
      `api_key=${process.env.GIPHY_API_TOKEN}&`,
      `q=${search}&`,
      `limit=${limit}&`,
      `offset=${offset}&`,
      `rating=${rating}&`,
      `lang=${lang}`].join('')
    )
  } catch(e) {
    console.log('Error: ', e);
    return;
  }

  resp.data.data.forEach(image => transformKey(image, ['images', '480w_still'], 'four80_w_still'))

  console.log({
    pagination: resp.data.pagination,
    analytics: resp.data.analytics,
    count: resp.data.length,
    results: resp.data
  })

  return {
    data: {
      pagination: resp.data.pagination,
      count: resp.data.data.length,
      results: resp.data.data
    }
  };
};
```

**RandomUserEnrich**

1. Go ahead and change return type in the `handler.ts` file to any (delete the return type)
2. Look at docs and land on specifying "nationality"
3. Next, hit the endpoint in the browser and let's inspect the JSON response and only pull out the fields that we care about.
4. Next, hop back to the `handler.ts` file and lets work with what we got.
5. 

```tsx
// request.json
{
    "data": {
      "nationality": "GB"
    }
}
```

```tsx
// schema.graphql

type RandomUserName {
  title: String,
  first: String,
  last: String
}

type RandomUserDob {
  date: DateTime,
  age: String
}

type RandomUserResolverResult {
  name: RandomUserName,
  dob: RandomUserDob,
  gender: String,
  email: String,
  phone: String,
  cell: String,
  nat: String
}

extend type Query {
  randomUserEnrich(nationality: String!): RandomUserResolverResult
}
```

```tsx
// handler.ts
import axios from 'axios';

export default async (event: any, ctx: any) : Promise<any> => {
  const { nationality } = event.data;

  let resp;

  try {
    resp = await axios.get(`https://randomuser.me/api/?nat=${nationality}`)
  } catch(e) {
    console.error(e)
    return;
  }

  let {
    id,
    login,
    picture,
    location,
    registered,
    ...randomUserAttrs
  } = resp.data.results[0]

  return {
    data: randomUserAttrs
  };
};
```

**AT THIS POINT, LETS DEPLOY FOR A TEST.**

```tsx
# Run deploy
8base deploy
```

While uploading, talk about how this is added these functions to lambda. Any typescript is being compiled. Also, will be able to use these on the GraphQL API.

Go back to the console and explore the API. Testing these calls.

```tsx
// GraphQL Test Call
query {
  giphySearch(q: "laughing") {
    results {
      url
      title
    }
  }
  
  randomUserEnrich(nationality: "ES") {
    name {
      first
      last
    }
    phone
  }
}
```

**enrichAndWelcome**

1. Go add and user to the Database (random user with fake email). Get their email.
2. Add that id to the request.json file.
3. Now hop into API Explorer and build an userUpdate mutation. The fields we want are:
    
    

```tsx
  mutation(
    $gender: String,
    $first: String,
    $last: String,  
    $date: String, 
    $cell: String,
    $id: ID
  ) {
    userUpdate(data: {
      id: $id
      firstName: $first
      lastName: $last
      gender: $gender
      birthday: $date
      cellPhone: $cell
      posts: {
        create: [{
          title: "Welcome to the app!",
          body: "We're so excited to have you here.",
        }]
      }
    }) {
      id
    }
  }
```

```tsx
// request.json (SWAP WITH AN ACTUAL USER ID)
{
  "data": {
    "id": "ck4ca7hqi005c08l96c0legjb"
  },
  "headers": {
    "x-header-1": "header value"
  }
}
```

```tsx
// Handler.ts

const UPDATE_USER_MUTATION = `
mutation(
  $gender: String,
  $first: String,
  $last: String,  
  $date: DateTime, 
  $cell: String,
  $id: ID
) {
  userUpdate(data: {
    id: $id
    firstName: $first
    lastName: $last
    gender: $gender
    birthday: $date
    cellPhone: $cell
    posts: {
      create: [{
        title: "Welcome to the app!",
        body: "We're so excited to have you here.",
      }]
    }
  }) {
    id
  }
}
`;

const ENRICH_USER_QUERY = `
  query($nat: String!) {
    randomUserEnrich(nationality: $nat) {
      name {
        first
        last
      }
      dob {
        date
      }
      gender
      cell
    }
  }
`;

export default async (event: any, ctx: any) : Promise<any> => {  
  let { id } = event.data;
  let errors: Error[] = [];
  let nat = 'GB';

  try {
    let { randomUserEnrich } = await ctx.api.gqlRequest(ENRICH_USER_QUERY, { nat })
    await ctx.api.gqlRequest(UPDATE_USER_MUTATION, { 
      first: randomUserEnrich.name.first,
      last: randomUserEnrich.name.last,  
      date: randomUserEnrich.dob.date, 
      gender: randomUserEnrich.gender,
      cell: randomUserEnrich.cell,
      id
    })
  } catch (e) {
    errors.push(e)
  }

	return {
    data: {
      ...event.data
    },
    errors
  }
};
```

**Create and Setup the Vue app**

1. Move all the "backend" code into a directory called `backend` and then clone the vue starter app into a directory called front-end.

```tsx
# Get Vue starter app
git clone frontend

# Move into the frontend
cd frontend && yarn
```

Talk about how this starter app is pre-wired and only needs environment variables. We need to set. **MAKE SURE THAT THE ALLOWED ORIGIN IS SET TO LOCALHOST:3000**

```tsx
VUE_APP_WORKSPACE_ENDPOINT=<YOUR_WORKSPACE_ENDPOINT>
VUE_APP_AUTH_PROFILE_ID=<YOUR_AUTH_PROFILE_ID>
VUE_APP_AUTH_CLIENT_ID=<YOUR_CLIENT_ID>
VUE_APP_AUTH_DOMAIN=<YOUR_AUTH_DOMAIN>

# Boot er up!
yarn serve
```

Now boot up the application. When we go to sign in, **USE THE SAME TEST USER EMAIL** as before. If this step gets missed, either open a Cognito window or make sure Evgeny has switched us to an 8base plan so that open sign-up can be used. **MAKE SURE THE USER HAS THE APPUSER ROLE!**

Let's update the Random Query in src/utils/graphql.js.

```tsx
// graphql.js

export const RANDOM_QUERY = gql`
query($search: String!) {
    user {
      firstName
      lastName
      cellPhone
      birthday
      posts {
        items {
          title
          body
        }
      }
    }
    
    giphySearch(q: $search, limit: 1) {
      results {
        images {
          downsized_medium {
            url
          }
        }
      }
    }
  }
`;
```

Update home.vue file to have the following mounted method.

```tsx
// Home.vue

mounted() {
    if (this.authenticated) {
      graphqlClient.query({ 
        query,
        variables: { 
          search: 'hello!' 
        }
      }).then(resp => (this.data = resp.data));
    }
  }
```

Develop the Home.vue component to show the data when authenticated.

```tsx
<template>
  <!-- Authenticated home view -->
  <div v-if="authenticated && data">
    <h1>You're Logged in!</h1>

    <img :src="data.giphySearch.results[0].images.downsized_medium.url" alt="Hello!" />

    <ul>
      <li><strong>Name: </strong> {{ data.user.firstName}} {{ data.user.lastName}}</li>
      <li><strong>Birthday: </strong> {{ data.user.birthday}}</li>
      <li><strong>Cell: </strong> {{ data.user.cellPhone}}</li>
    </ul>

    <ul>
      <li><strong>Posts</strong></li>
      <li v-for="(p, i) in data.user.posts.items" :key="i">
        <h5>{{p.title}}</h5>
        <p>{{p.body}}</p>
      </li>
    </ul>
  </div>

  <h1 v-else>
    You need to login!
  </h1>
</template>

<script>
/* Import packages */
import { mapGetters } from "vuex";
import graphqlClient from "@/utils/api";
import { RANDOM_QUERY as query } from "@/utils/graphql";

export default {
  name: "home",
  data() {
    return {
      data: undefined
    };
  },
  /**
   * Use state getters and actions to manage display
   * of baords are reflect mutations.
   */
  computed: {
    prettifyResp() {
      return JSON.stringify(this.data, undefined, 2);
    },
    ...mapGetters(["authenticated"])
  },
  mounted() {
    if (this.authenticated) {
      graphqlClient.query({ 
        query,
        variables: { 
          search: 'hello!' 
        }
      }).then(resp => (this.data = resp.data));
    }
  }
};
</script>
```

**BONUS EXTRA**

Plugins

We're going to tighten this up soon, as we're just testing it, but plugins.

```tsx
# Make plugin
8base g plugin giphy

# Move the search code to the giphy plugin src 
# directory and change the name to search.

# Make sure the schema.grapql file type is GiphyQuery!

# Inside the plugin folder
npm install

# Deploy
8base deploy --mode=FULL

# Explain how this is now a packaged thing, where it's neatly namespaced.
```
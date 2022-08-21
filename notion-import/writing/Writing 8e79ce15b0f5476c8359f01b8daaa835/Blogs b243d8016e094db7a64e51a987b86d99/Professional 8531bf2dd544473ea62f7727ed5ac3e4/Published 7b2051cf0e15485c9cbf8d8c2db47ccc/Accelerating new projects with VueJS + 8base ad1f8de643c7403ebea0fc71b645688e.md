# Accelerating new projects with VueJS + 8base

There’s a directory named ***graveyard*** at the root path of my computer. It’s where my dreams go to die!

That’s morbid. Excuse me; it’s where I move projects that I’m no longer actively working on. It keeps my working directories slim and organized.

The other day, I went rummaging around my graveyard. Over two-dozens applications and components are collecting dust in there! Most of them are ideas I impulsively initialized and soon after forgot about, while — deep down — several of them I still consider *tickets out of dodge*.

Nonetheless, each project’s name reminded me of a “big idea” I had. However, as I looked through the code files, an awful pattern emerged.

Most projects in my graveyard are shells, which means that I never got around to developing the original idea. Instead, the time spent on each project went into systems like auth, databases, APIs, file uploads, etc.

Do I have commitment issues? Maybe. That said, I decided to start **another** project that might help me going forward. It’s a starter app that has all the shared requirements of my graveyard projects ready to go. Those requirements are:

- **User Authentication (Sign Up, Sign In, Forgot Password, etc…)**
- **API (Aurora MySQL Database, GraphQL API, Image Uploads/S3 Storage)**
- **Roles/Permissions (JWT Authorization with resource scoping and action level permissions)**
- **Client (VueJS PWA with Router + VueX state management)**

After a few test-drives, I was able to get a new app up and running in less than 5-minutes! Here is the [Starter App](https://github.com/8base/vue-8base-starter-app), the *this* is how it works.

# The Breakdown

As you’ve likely gathered at this point, this “Starter App” is for kick-starting a web application project. Of all the hip frameworks, I personally love VueJS. Therefore, I started by initializing a new VueJS project using their CLI tool.

If you want to generate the app from scratch, you **could** do so! However, to follow along, clone the repo using Git.

**Clone the Project**

An *.env* file is located at the root of the project so that credentials and keys can safely get added to the project. It asks for an 8base workspace endpoint and authentication profile credentials. Let’s set those up now.

# Server Setup

1. Login to [app.8base.com](https://app.8base.com/)
2. Copy *API Endpoint* (a.k.a, workspace endpoint). Go ahead and set this in the .env file.
3. Navigate to [app.8base.com/settings/authentication](https://app.8base.com/settings/authentication) and add a new *Authentication Profile*.

![Accelerating%20new%20projects%20with%20VueJS%20+%208base%20ad1f8de643c7403ebea0fc71b645688e/4da35a0ddc55d870b108f9d9ae7278ff.jpg](4da35a0ddc55d870b108f9d9ae7278ff.jpg)

1. Name it (e.g., “Default Auth”)
2. Select “8base Authentication” as *Type*
3. Select “Open to All” as *Self Signup*
4. Select “Guest” as *Roles*
5. Add the Profile!
6. The *Client ID, Domain,* and *Authentication Profile ID* all belong in the .env file.
7. Lastly, make sure *Custom Domains* has https:localhost:**8080** as URL host in values.

# Front-end Setup

With the values that are now stored in the .env file, the app is fully configured to sign-up/authenticate users and then securely communicate with the 8base workspace GraphQL API…

***BUT HOW?!?!***

First and foremost, let’s look at our *Auth* module (*src/utils/auth.js*). We’re only creating a new instance of the 8base SDK’s Auth class. Its configuration accepts the environment variables that are already set, and logout/redirect URLs from the *Authentication Profile.* Pretty straightforward!

We make use of this auth client in the Vuex sessions module (*src/store/modules/session.js*). Stored in the actions object there are *login, logout,* and *handleAuthentication* methods. These methods make use of the auth client module.

The auth client loads a hosted authentication page when *authorize* is called. When the user successfully authenticates, it redirects them back to the specified *redirectUrl*. In the *Router* (*src/router.js*), we’ve defined a path to handle that authentication callback.

When the Callback component loads, the *mounted* life-cycle hook runs. Inside that method, the *handleAuthentication* method is called, which brings us right back to our Vuex session module.

The *handleAuthentication* method uses the auth client to retrieve the authorized user’s data. Things like the user’s *email* and *idToken* are returned. The returned ID token gets used to authenticate a request to the 8base GraphQL API and see if the authenticated user exists. If they do, excellent; if not, they’re added as a new user! Lastly, the authResult gets added to the state.

Awesome! Users can authenticate, and we understand why. Let’s take a look at the API module.

Instead of having to import packages into different components, as well as worry about auth headers and error handling, we’ve created a single API module. The API module (*src/utils/api.js*) gets imported into Vuex modules, and anywhere else, to communicate with the workspace API. 8base provisions workspaces with a GraphQL API through which users can query data.

Using various Apollo packages, an *ApolloClient* instance gets constructed using the workspace endpoint stored in the .env file. The *authLink* constant sets the user *idToken* as a bearer **token header in requests, ensuring that API calls are authorized.

If you keep snooping around, you’ll find the *utils/graphql.js* file that has all the *queries* neatly organized. You’ll find examples (like, *src/views/Profile.vue*) where the API module and *CURRENT_USER_QUERY* are imported to fetch data for a profile page. There’s plenty of nuggets sprinkled throughout the project that — hopefully — will help you handle whatever your next project demands!

# Conclusion

It would be so cool if we could **only** work on our ideas. What do I mean by that? Imagine if you could start a project or company, but didn’t have any busy work. Instead, that was just done for you.

After looking through my graveyard, I felt like I had lost my spark on many projects because I wasn’t actually getting to focus on *them*! My hours got spent doing things I didn’t enjoy. So, I found something else to do.

All that said, I hope this starter app helps you kick off a fantastic project of your own! It’s open-source, so feel free to submit changes via pull requests :)
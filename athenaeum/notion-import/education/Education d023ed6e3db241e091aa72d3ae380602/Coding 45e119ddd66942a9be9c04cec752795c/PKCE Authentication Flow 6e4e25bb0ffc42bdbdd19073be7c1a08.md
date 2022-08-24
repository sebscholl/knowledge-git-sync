# PKCE Authentication Flow

Last Edited: December 19, 2019 11:43 PM

import crypto from 'crypto'

import * as queryString from 'query-string'

import { domain, clientId } from './utils/init'

import * as requestPromise from 'request-promise'

const base64URLEncode = (str) => {

return str.toString('base64')

.replace(/\+/g, '-')

.replace(/\//g, '_')

.replace(/=/g, '')

}

const sha256 = (buffer) => {

return crypto.createHash('sha256').update(buffer).digest()

}

// Authorization Code with PKCE is the OAuth 2.0

// grant that native applications use in order

// to access an API.

export default class AuthCodePKCE {

// The verifier and the challenge need to be stored

// for subsequent requests. Make sure to keep a reference

// to the AuthCodePKCE instance during grant flow

constructor () {

this.verifier = base64URLEncode(crypto.randomBytes(32))

this.challenge = base64URLEncode(sha256(this.verifier))

}

// Generate link to send the user to the authorization URL including

// the code_challenge and the method used to generate it

authorizationUrl () {

return `https://${domain}/authorize?${queryString.stringify({

redirect_uri: `[rampex://desktop-gym.com/auth](rampex://desktop-gym.com/auth)`,

code_challenge: this.challenge,

code_challenge_method: 'S256',

audience: 'rampex-rails/api',

scope: 'read:simulations',

response_type: 'code',

client_id: clientId

})}`

}

// Exchange code for an Access Token that can be used to call your API.

// Using the Authorization Code (code) from the previous step, you will

// need to POST to the Token URL sending also the code_verifier

fetchAccessToken (code) {

return requestPromise({

method: 'POST',

uri: `https://${domain}/oauth/token`,

body: {

redirect_uri: `[rampex://desktop-gym.com/auth](rampex://desktop-gym.com/auth)`,

grant_type: 'authorization_code',

code_verifier: this.verifier,

client_id: clientId,

code: code

},

json: true

})

}

}
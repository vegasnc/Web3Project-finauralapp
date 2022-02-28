<br/>
<a href="https://finaural.com" target="_blank"><img src="https://finaural.com/img/finaural.png"/></a>
<br/><br/>
Finaural creates high quality audio masters to give musicians and creators the opportunity to focus on their content while obtaining the best sound experience at all times.

<br/>

# Application

We utilise machine learning models in a mighty application to analyse, process and deliver your files in seconds.

<br/>

## Backend Server
Built with <a href="https://docs.nestjs.com" target="_blank">NestJS</a>.

<details>
<summary>Framework</summary>

#### Install NestJS

```
npm i -g @nestjs/cli
nest new backend
cd backend
npm install
npm run start
```

<details>
<summary>Installed Add-ons</summary>

#### Hot Reload
<a href="https://docs.nestjs.com/recipes/hot-reload" target="_blank">Recipes: Hot Reload</a>
<br/>
Dependencies:
<br/>
```
npm i --save-dev webpack-node-externals run-script-webpack-plugin webpack
```
</details>

</details>

<details>
<summary>API (todo)</summary>

#### Dependencies for GraphQL & Apollo
```
npm i @nestjs/graphql @nestjs/apollo graphql apollo-server-express
```
</details>

<details>
<summary>Authorization (todo)</summary>

#### Implement Web3 Authorization
```

```
</details>

<details>
<summary>File System (todo)</summary>

#### Implement File System access
```

```
</details>
<br/>

## Frontend Server
Built with <a href="https://kit.svelte.dev" target="_blank">Sveltekit</a>.

### Basic Setup

<details>
<summary>Framework</summary>

#### Install Sveltekit & TailwindCSS

```
cd / && npm init svelte@next frontend -y
cd frontend
npm install
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init tailwind.config.cjs -p
mv postcss.config.js postcss.config.cjs
```

```
nano ./tailwind.config.cjs
module.exports = {
  content: ['./src/**/*.{html,js,svelte,ts}'],
  theme: {
    extend: {}
  },
  plugins: []
};
```

```
nano ./src/app.css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```
nano ./src/routes/__layout.svelte
<script>
  import "../app.css";
</script>
<slot />
```
</details>

<details>
<summary>Adapter</summary>

#### Deploy Svelte via Node
```
npm i @sveltejs/adapter-node@next
```
```
// svelte.config.js
-import adapter from '@sveltejs/adapter-auto';
+import adapter from '@sveltejs/adapter-node';
```
```
// package.json
-"@sveltejs/adapter-auto": "next",
+"@sveltejs/adapter-node": "next",
```
</details>

<details>
<summary>Auth0 (deprecated)</summary>

### Add Auth0 & initialize stores 
```
npm install @auth0/auth0-spa-js
```
```
nano ./src/store.js
import { writable, derived } from "svelte/store";
export const isAuthenticated = writable(false);
export const user = writable({});
export const popupOpen = writable(false);
export const error = writable();
export const tasks = writable([]);
export const user_tasks = derived([tasks, user], ([$tasks, $user]) => {
  let logged_in_user_tasks = [];
  if ($user && $user.email) {
    logged_in_user_tasks = $tasks.filter((task) => task.user === $user.email);
  }
  return logged_in_user_tasks;
});
```
```
nano ./auth_config.js
const config = {
  domain: "YOUR_AUTH0_DOMAIN",
  clientId: "YOUR_APP_CLIENT_ID"
};
export default config;
```
```
nano ./src/authService.js
import createAuth0Client from "@auth0/auth0-spa-js";
import { user, isAuthenticated, popupOpen } from "./store";
import config from "../auth_config";
async function createClient() {
  let auth0Client = await createAuth0Client({
    domain: config.domain,
    client_id: config.clientId
  });
  return auth0Client;
}
async function loginWithPopup(client, options) {
  popupOpen.set(true);
  try {
    await client.loginWithPopup(options);
    user.set(await client.getUser());
    isAuthenticated.set(true);
  } catch (e) {
    // eslint-disable-next-line
    console.error(e);
  } finally {
    popupOpen.set(false);
  }
}
function logout(client) {
  return client.logout();
}
const auth = {
  createClient,
  loginWithPopup,
  logout
};
export default auth;
```
</details>

<br/>

## Processing Unit

The processing unit is in a Pre-alpha stage.



<br/>

___

<br/>
<a href="github_url" target="_blank"><img src="github_image"/></a> Join our Discord Server
<br>
<a href="discord_url" target="_blank"><img src="discord_image"/></a> Follow us on Github
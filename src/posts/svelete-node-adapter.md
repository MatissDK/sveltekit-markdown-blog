---
title: Svelte node adapter inside docker container
description: Deploy sveltekit app to server.
date: '2023-12-29'
categories:
  - sveltekit
  - svelte
  - docker
  - github actions
published: true
---

Hello friends! 👋

Successfully running your app locally is only a portion of the victory; the other crucial aspect is deploying it to a live server. As outlined in the SvelteKit documentation: 'Before you can deploy your SvelteKit app, you need to adapt it for your deployment target.' In my case, the goal for this project was to deploy it on my Linode standalone server. The logical choice for this deployment scenario was the @sveltejs/adapter-node.

## Step 1: Install the Node Adapter


```shell:terminal
  npm i -D @sveltejs/adapter-node
```

After the installation, don't forget to update your package.json and remove @sveltejs/adapter-auto dependency from package.json file

```ts
{
 	"devDependencies": {
		"@sveltejs/adapter-auto": "^3.0.0",
		"@sveltejs/adapter-node": "^2.0.2"
  }
}
```

## Step 2: Configure the Adapter in your svelte.config.js.

Replace @sveltejs/adapter-auto with @sveltejs/adapter-node

```ts
 import adapter from '@sveltejs/adapter-node';

 export default {
    kit: {
      adapter: adapter()
    }
  };
```

## Step 3: Validate Your App

Before deploying, it's crucial to ensure your app is running smoothly. Build the app by executing:

```shell:terminal
  npm run build
```

This command will generate the /build folder. To launch your app, use:

```bash
  node build
```

You should see a message like: Listening on 0.0.0.0:3000, indicating that the server is running on port 3000.

```ts
FROM node:18-alpine AS builder

RUN mkdir /app

COPY . /app

RUN cd /app && npm install && \
  npm run build


FROM node:18-alpine

RUN mkdir /app

COPY --from=builder /app/build /app/build
COPY --from=builder /app/package.json /app/package-lock.json /app/

  RUN cd /app && \ 
  npm install --production

WORKDIR /app

EXPOSE 3000

CMD ["node", "build/index.js"]
```

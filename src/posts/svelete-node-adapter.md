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

## Markdown

Hey friends! 👋

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

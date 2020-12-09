# Cats Card App

  

Hi! 
This app, built with **Vue** and **Nuxt**, retrieves data from https://docs.thecatapi.com and displays it with dynamic pagination and some category selection.

It also features lazy loading with the help of the **Intersection Observer API**

## Commands

  

```bash

# install dependencies

$ npm install

# serve with hot reload at localhost:3000

$ npm run dev

# build for production and launch server

$ npm run build

$ npm run start

# generate static project

$ npm run generate

```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).

Main components:
```mermaid

graph LR

A[CardList] --> B(Pagination)

A --> C(CategorySelect)

A -- Api data --> D(Card / v-for loop)

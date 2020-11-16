# Book review app

This app was made for [this blog post](https://dgraph.io/blog/post/build-a-svelte-urql-app-with-slash-graphql/), in which we learn "How to build a book review app with Svelte, urql and Slash GraphQL".

The blog post teaches you how to build a GraphQL app with:

* [urql](https://formidable.com/open-source/urql/): a lightweight GraphQL client from [Formidable Labs](https://formidable.com/); 
* [Svelte](https://svelte.dev/): a radical new javascript framework for building user interfaces; and
* [Slash GraphQL](https://dgraph.io/slash-graphql): Dgraph’s managed GraphQL backend service. 

Slash GraphQL lets you build GraphQL apps without worrying about deployments or translating to GraphQL from other storage domains - it’s just GraphQL, start to finish.

Clone the repo with.

```bash
git clone https://github.com/dgraph-io/svelte-urql-example.git
cd svelte-urql-example
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*

## Get started

[The accompanying blog post](https://dgraph.io/blog/post/build-a-svelte-urql-app-with-slash-graphql/) tells you how to get yourself a Slash GraphQL account and deploy a GraphQL backend for this example app.

Then, install the dependencies...

```bash
cd svelte-urql-example
npm install
```

Edit `src/App.svelte`, on line 12 replace "YOUR-SLASH-ENDPOINT" with your Slash GraphQL endpoint.

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. 

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

<script>
  import { Router, Route, Link } from "svelte-routing";
  import Home from "./components/Home.svelte";
  import Book from "./components/Book.svelte";
  import Author from "./components/Author.svelte";
  import Review from "./components/Review.svelte";

  export let url = "";
  import { initClient } from "@urql/svelte";

  initClient({
    url: "YOUR-SLASH-ENDPOINT"
  });
</script>

<Router {url}>
  <nav>
    <Link to="/">Home</Link>
  </nav>

  <div>
    <Route path="/">
      <Home />
    </Route>
    <Route path="book/:id" let:params>
      <Book id={params.id} />
    </Route>
    <Route path="author/:name" let:params>
      <Author name={params.name} />
    </Route>
    <Route path="review/:id" let:params>
      <Review id={params.id} />
    </Route>
  </div>
</Router>

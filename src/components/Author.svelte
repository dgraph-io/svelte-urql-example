<script>
  import { Router, Route, Link } from "svelte-routing";

  export let name = "";
  import { operationStore, query } from "@urql/svelte";

  const author = operationStore(
    `
   query($name: String!) {
  getAuthor(name: $name) {
    name
    description
    books {
          id
    name
    genre
    author {
      name
    }
    }
  }
}
  `,
    { name }
  );
  query(author);
</script>

<style>
  .grid-container {
    display: grid;
    grid-template-columns: auto auto auto;
    background-color: #2196f3;
    padding: 10px;
  }
  .grid-item {
    background-color: rgba(255, 255, 255, 0.8);
    border: 1px solid rgba(0, 0, 0, 0.8);
    padding: 20px;
    font-size: 30px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    transition: 0.3s;
    margin: 8px;
  }
  .grid-item:hover {
    box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
  }
</style>

<main>
  <h1>Author</h1>
</main>
<div>
  {#if $author.fetching}
    Loading...
  {:else if $author.error}
    Oh no! {$author.error.message}
  {:else if !$author.data}
    No data
  {:else}
    <div>Name - {$author.data.getAuthor.name}</div>
    <div>Description - {$author.data.getAuthor.description}</div>
    <div class="grid-container">
      {#each $author.data.getAuthor.books as book}
        <div class="grid-item">
          <div>
            Name -
            <Link to={`book/${book.id}`}>{book.name}</Link>
          </div>
          <div>Author - {book.author.name}</div>
          <br />
          <div>
            <Link to={`review/${book.id}`}>Submit Review</Link>
          </div>
        </div>
      {/each}
    </div>
  {/if}
</div>

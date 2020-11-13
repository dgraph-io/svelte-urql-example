<script>
  import { Link } from "svelte-routing";
  import { operationStore, query } from "@urql/svelte";

  const books = operationStore(
    `
   {
  queryBook {
    id
    name
    genre
    author {
      name
    }
  }
}
  `
  );
  query(books);
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
  <h1>Welcome to Books App</h1>
</main>
<div>
  {#if $books.fetching}
    Loading...
  {:else if $books.error}
    Oh no! {$books.error.message}
  {:else if !$books.data}
    No data
  {:else}
    <div class="grid-container">
      {#each $books.data.queryBook as book}
        <div class="grid-item">
          <div>
            Name -
            <Link to={`book/${book.id}`}>{book.name}</Link>
          </div>
          <div>
            Author -
            <Link to={`author/${book.author.name}`}>{book.author.name}</Link>
          </div>
        </div>
      {/each}
    </div>
  {/if}
</div>

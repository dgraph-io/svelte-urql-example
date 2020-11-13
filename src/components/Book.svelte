<script>
  import { Router, Route, Link } from "svelte-routing";

  export let id = "";
  import { operationStore, query } from "@urql/svelte";

  const book = operationStore(
    `
   query($id: ID!) {
  getBook(id: $id) {
    id
    name
    genre
    author {
      name
    }
    reviews {
      id
      postedBy {
        username
      }
      text
      rating
    }
  }
}
  `,
    { id },
    { requestPolicy: "network-only" }
  );
  query(book);
</script>

<style>
  .grid-container {
    display: block;
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
  }
  .grid-item:hover {
    box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
  }
</style>

<main>
  <h1>Book</h1>
</main>
<div>
  {#if $book.fetching}
    Loading...
  {:else if $book.error}
    Oh no! {$book.error.message}
  {:else if !$book.data}
    No data
  {:else}
    <div class="grid-container">
      <div class="grid-item">
        <div>Name - {$book.data.getBook.name}</div>
        <div>
          Author -
          <Link to={`author/${book.data.getBook.author.name}`}>
            {$book.data.getBook.author.name}
          </Link>
          <div>
            {#if $book.data.getBook.reviews.length != 0}
              <div>Reviews - </div>
            {/if}
            {#each $book.data.getBook.reviews as review}
              <div class="grid-item">
                <div>Rating - {review.rating}</div>
                <div>Text - {review.text}</div>
                <div>Username - {review.postedBy.username}</div>
              </div>
            {/each}
          </div>
          <hr />
          <div>
            <Link to={`review/${book.data.getBook.id}`}>Submit Review</Link>
          </div>
        </div>
      </div>
    </div>
  {/if}
</div>

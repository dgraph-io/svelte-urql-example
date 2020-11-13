<script>
  import { mutation } from "@urql/svelte";
  import { navigate } from "svelte-routing";

  export let id;
  let rating = 2;
  let username = "";
  let review = "";

  const mutateReview = mutation({
    query: `
      mutation ($input: [AddReviewInput!]!) {
        addReview (input: $input) {
          numUids
        }
      }
    `
  });
  function addReview() {
    const reviewObject = [
      {
        text: review,
        rating: rating,
        postedBy: { username: username },
        reviewedBook: { id: id }
      }
    ];
    mutateReview({ input: reviewObject }).then(result => {
      navigate(`/book/${id}`);
    });
  }
</script>

<style>
  .content {
    display: grid;
    grid-template-columns: 20% 80%;
    grid-column-gap: 10px;
    padding-right: 10px;
  }
  .btn {
    text-align: center;
  }
</style>

<main>
  <h1>Review</h1>
</main>

<div class="content">
  <label for="username">Username</label>
  <input bind:value={username} id="username" />
  <label for="rating">Rating</label>
  <input type="number" bind:value={rating} min="0" max="5" id="rating" />
  <label for="text">Text</label>
  <textarea bind:value={review} id="text" />
</div>

<div class="btn">
  <button on:click={addReview}>Submit</button>
</div>

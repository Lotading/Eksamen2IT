<script>
  import { Collection } from "sveltefire";
</script>

<Collection ref={"faq"} let:data let:count>
  <h1>Tidligere problemer</h1> 
  <p>Her kan du se problemer og svar til andre</p>
  {#each data as post}
    <p class="w-1/3 border-white border-2 my-2 rounded-xl flex justify-self-center px-2">{post.problem}</p>
  {/each}
</Collection>

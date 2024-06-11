<script>
  import { Collection } from "sveltefire";
</script>

<Collection ref={"faq"} let:data let:count>
  <p>previous issues</p>
  <p>fan t {count} problemer</p>

  {#each data as post}
    <p class="w-1/3 border-white border-2 my-2 rounded-xl">{post.problem}</p>
  {/each}
</Collection>

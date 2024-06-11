<script>
  import { ref } from "firebase/database";
  import { Collection } from "sveltefire";
  
</script>

<section>
  <h1>Kjop Dekk hos oss!</h1>
  <Collection ref={"products"} let:data>
    {#each data as posts}
      <div>
        <p>{posts.name}</p>
        <p>{posts.description}</p>
        <p>{posts.price}</p>
      </div>
    {/each}
  </Collection>
</section>

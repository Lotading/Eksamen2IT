<script>
  import { Collection } from "sveltefire";
  import images from '$lib/images.jpg'
</script>

<section>
  <h1 class="text-white text-5xl my-2 mb-3 ml-2">Kjop Dekk hos oss!</h1>
  <span class="flex flex-row space-x-2">
  <Collection ref={"products"} let:data>
    {#each data as posts}
      <div class="border-white border-2 mx-2 w-auto rounded-2xl">
      <!-- svelte-ignore a11y-missing-attribute -->
      <img src={images} alt="poo" class='w-auto h-auto rounded-t-2xl'>
        <div class="bg-base rounded-b-2xl">
          <p class="border-t-2 border-white">{posts.name}</p>
          <p>{posts.description}</p>
          <p>{posts.price}</p>
          <button class="border-t-2 border-white w-full" on:click={() => {alert('Ditt kjop er klargjort')}}>Kjop</button>
        </div>
      </div>
    {/each}
  </Collection>
  </span>
</section>

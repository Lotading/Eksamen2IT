<script>
  import { Collection } from "sveltefire";
  import { addDoc, collection } from 'firebase/firestore'
  import { firestore } from "$lib/firebase";

  let product = {
    description: '',
    name: '',
    pris: '',
  }

  const sendData = () => {
    addDoc(collection(firestore,'products'),product)
    product.description = '';
    product.name = '';
    product.pris = '';
  }
</script>

<section class="justify-center flex">
  <form class="flex-col flex w-1/3 space-y-2 mt-5">
    <p class="text-xl">Legg til et produkt i butikken:</p>
    <input type="text" bind:value={product.name} placeholder="navn" class="text-base border-white">
    <input type="text" bind:value={product.description} placeholder="info om produkt" class="text-base">
    <input type="text" bind:value={product.pris} placeholder="pris" class="text-base">
    <button type="submit" class="bg-base border-white border-2 mx-2 px-2 rounded-md" on:click={sendData}>Lag produkt</button>
  </form>
</section>


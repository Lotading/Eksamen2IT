<script>
  import { firestore } from "$lib/firebase";
  import { collection } from "firebase/firestore";
  import { addDoc } from "firebase/firestore";
  import { Collection } from "sveltefire";

  let data = {
    date: "",
    time: "",
    navn: "",
    email: "",
  };

  const sendInfo = () => {
    addDoc(collection(firestore, "vaskehall"), data);
    alert("Din bestilling er klargjort");
    data.navn = "";
    data.email = "";
    data.date = "";
    data.time = "";
  };
</script>

<div
  class="flex space-y-2 mt-2 flex-col space-x-4 place-items-center justify-center"
>
  <form class="flex flex-col space-y-2 w-1/3">
    <input
      placeholder="Navn"
      type="text"
      bind:value={data.navn}
      class="border-white border-2 w=1/3 text-base"
      required
    />
    <input
      type="email"
      placeholder="Email"
      bind:value={data.email}
      class="border-white border-2 w=1/3 text-base"
      required
    />
    <select
      bind:value={data.date}
      placeholder="Dag"
      class="border-white border-2 text-base"
    >
      <option disabled selected hidden>Dag</option>
      <option value="Mandag">Mandag</option>
      <option value="Tirsdag">Tirsdag</option>
      <option value="Onsdag">Onsdag</option>
      <option value="Torsdag">Torsdag</option>
      <option value="Fredag">Fredag</option>
      <option value="Lordag">Lordag</option>
      <option value="Sondag">Sondag</option>
    </select>

    <p>Klokkeslett:</p>
    <input
      type="time"
      bind:value={data.time}
      required
      class="border-white border-2 text-base"
    />
    <button
      type="submit"
      on:click={sendInfo}
      class="w-1/3 border-2 bg-green-500 mx-2 px-2 rounded-md bg-base">Send in Bestilling</button
    >
  </form>
  <section class="w-1/3 flex flex-col border-cwhite bg-surface rounded-xl border-2 space-y-2 align-items-center space-x-2">
    <h1 class="w-full bg-base rounded-t-xl border-b-2">Bestilte timer</h1>
    <Collection ref={"vaskehall"} let:data>
      {#each data as posts}
        <div class="flex-row flex space-x-2 justify-items-center content-center rounded-sm">
          <p>Navn: {posts.navn}</p>
          <p>Dag: {posts.date}</p>
          <p>Tid: {posts.time}</p>
        </div>
      {/each}
    </Collection>
  </section>
</div>

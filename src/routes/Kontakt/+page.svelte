<script>
  let data = {
    problem: "",
    email: "",
    res: "Skru maskin av og paa",
  };

  import { firestore } from "$lib/firebase";
  import { addDoc } from "firebase/firestore";
  import { collection } from "firebase/firestore";

  const sendData = () => {
    addDoc(collection(firestore, "faq"), data);
    alert("Hei, takk for at du tar konakt, vi skal se paa det!");
    data.email = "";
    data.problem = "";
  };
</script>
<div class="justify-center items-center flex mt-10">
  <div class="flex-col flex w-1/3 justify-self-center space-y-1">
    <label for="emailKontakt" class="text-xl"
      >Har du noen spørsmål? Ta gjerne kontakt under!</label
    ><br />
    <input
      type="text"
      placeholder="problem123"
      class="border-black border-2 text-base"
      bind:value={data.problem}
      required
    />
    <input
      type="email"
      id="emailKontakt"
      placeholder="john@doe.com"
      class="border-black border-2 text-base"
      bind:value={data.email}
      required
    />
    <button
      type="submit"
      class="border-white rounded-md border-2 px-2 bg-base text-white hover:bg-slate-300"
      on:click={sendData}>Send inn</button
    >
  </div>
</div>
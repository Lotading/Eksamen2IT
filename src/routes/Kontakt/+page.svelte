<script>
  let data = {
    problem: "",
    email: "",
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

<div>
  <label for="emailKontakt"
    >Har du noen spørsmål? Ta gjerne kontakt under!</label
  ><br />
  <input
    type="text"
    placeholder="problem123"
    class="border-black border-2 text-black"
    bind:value={data.problem}
    required
  />
  <input
    type="email"
    id="emailKontakt"
    placeholder="john@doe.com"
    class="border-black border-2 text-black"
    bind:value={data.email}
    required
  />
  <button type="submit" class="border-black border-2 bg-white text-black hover:bg-slate-300" on:click={sendData}
    >Send inn</button
  >
</div>

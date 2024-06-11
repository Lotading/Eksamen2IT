<script lang="ts">
  import type { Auth } from "firebase/auth";

  import "../app.css";

  import { FirebaseApp } from "sveltefire";
  import { auth, firestore } from '$lib/firebase'

  import { GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";

  import {
    //    getFirebaseContext,
    //    userStore,
    SignedIn,
    SignedOut,
  } from "sveltefire";

  async function signInWithGoogle(auth: Auth) {
    const provider = new GoogleAuthProvider();
    provider.addScope("profile");
    provider.addScope("email");
    await signInWithPopup(auth, provider);
  }
</script>

<FirebaseApp {auth} {firestore}>
  <nav
    class="relative w-full border-b-2 border-white flex flex-row justify-between bg-slate-950 items-center p-4"
  >
    <div class="flex space-x-4">
      <a href="/" class="hover:underline text-2xl">Home</a>
      <a href="/Faq" class="hover:underline text-2xl">Faq</a>
      <a href="/Kontakt" class="hover:underline text-2xl">Kontakt</a>
      <a href="/Vaskehall" class="hover:underline text-2xl">Vaskehallen</a>
      <a href="/Shop" class="hover:underline text-2xl">Produkter</a>
    </div>
    <div >
      <!-- svelte-ignore a11y-missing-attribute -->
      <SignedOut>
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <!-- svelte-ignore a11y-no-static-element-interactions -->
        <a type="button" on:click={() => signInWithGoogle(auth)} class="hover:underline text-2xl"
          >Login</a
        >
      </SignedOut>
      <!-- svelte-ignore a11y-no-static-element-interactions -->
      <SignedIn let:user>
        <!-- svelte-ignore a11y-missing-attribute -->
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <a type="button" on:click={() => signOut(auth)} class="hover:underline text-2xl"
          >Sign out ({user.displayName}) |</a
        >
        <a href="/Admin" class="hover:underline text-2xl mx-1">Admin</a>
      </SignedIn>
    </div>
  </nav>

  <slot />

  <footer
    class="fixed border-t-2 border-white bottom-0 w-full text-center p-4 h-auto"
  >
    <p>All rights reserved BreiDekk&copy;</p>
  </footer>
</FirebaseApp>

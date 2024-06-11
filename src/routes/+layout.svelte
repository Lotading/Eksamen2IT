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
    class="relative w-full border-b-2 border-white flex flex-row justify-between items-center p-4"
  >
    <div class="flex space-x-4">
      <a href="/" class="hover:underline text-2xl">Home</a>
      <a href="/Faq" class="hover:underline text-2xl">Faq</a>
      <a href="/Kontakt" class="hover:underline text-2xl">Kontakt</a>
      <a href="/Vaskehall" class="hover:underline text-2xl">Vaskehallen</a>
    </div>
    <div>
      <SignedOut>
        <button on:click={() => signInWithGoogle(auth)} class="hover:underline"
          >Login</button
        >
      </SignedOut>
      <SignedIn let:user>
        <button on:click={() => signOut(auth)} class="hover:underline"
          >Sign out ({user.displayName})</button
        >
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

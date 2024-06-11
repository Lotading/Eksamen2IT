<script lang="ts">

import type { Auth } from 'firebase/auth'

import "../app.css";

import { FirebaseApp } from 'sveltefire'
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";

import {
    GoogleAuthProvider,
    signInWithPopup,
    signOut
} from 'firebase/auth'

import {
//    getFirebaseContext,
//    userStore,
    SignedIn,
    SignedOut
} from 'sveltefire'

import { getFirestore } from "firebase/firestore";

const config = {
  apiKey: "AIzaSyAW_h6RxSWm-tooaMSV3uL5fcYfQPRIRFM",
  authDomain: "eksamen2it.firebaseapp.com",
  projectId: "eksamen2it",
  storageBucket: "eksamen2it.appspot.com",
  messagingSenderId: "386575356551",
  appId: "1:386575356551:web:279fb15cda8e427a889e22",
  measurementId: "G-0338V8RWKS"
};

const app = initializeApp(config);
export const firestore = getFirestore(app);
export const auth = getAuth(app);

async function signInWithGoogle (auth: Auth) {
  const provider = new GoogleAuthProvider()
  provider.addScope('profile')
  provider.addScope('email')
  await signInWithPopup(auth, provider)
}
</script>

<FirebaseApp {auth} {firestore}>
    <nav class="relative w-full border-b-2 border-black flex flex-row justify-between items-center p-4">
      <div class="flex space-x-4">
        <a href="/" class="hover:underline text-2xl">Home</a>
        <a href="/Faq" class="hover:underline text-2xl">Faq</a>
      </div>
      <div>
        <SignedOut>
          <button on:click={() => signInWithGoogle(auth)} class="hover:underline">Login</button>
        </SignedOut>
        <SignedIn let:user>
          <button on:click={() => signOut(auth)} class="hover:underline">Sign out ({user.displayName})</button>
        </SignedIn>
      </div>
    </nav>

    <slot />
    
    <footer class="fixed border-t-2 border-black bottom-0 w-full text-center p-4 h-auto">
      <p>All rights reserved [blank]&copy;</p>
    </footer>
</FirebaseApp>

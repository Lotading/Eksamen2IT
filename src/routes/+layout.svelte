<script lang="ts">

import "../app.css";

import { FirebaseApp } from 'sveltefire'
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";
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

</script>

<FirebaseApp { auth } { firestore }>
    <nav class="border-b-2 border-black">
        <a href="/">Home</a>
        <a href="/Faq">Faq</a>
    </nav>

    <slot />
    
    <footer class="fixed flex bottom-0">
      <p>most gangster footer</p>
    </footer>
</FirebaseApp>
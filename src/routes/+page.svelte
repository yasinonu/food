<script lang="ts">
    import { FirebaseApp, collectionStore, docStore } from 'sveltefire';
    import { initializeApp } from 'firebase/app';
    import { getFirestore } from 'firebase/firestore';
    import { getAuth } from 'firebase/auth';
    import { SignedIn, SignedOut, Doc, Collection } from 'sveltefire';
    import { signInAnonymously } from "firebase/auth";
    import { Card, Button, Rating } from 'flowbite-svelte';
    import { setContext } from 'svelte';
    import { writable } from 'svelte/store';

    // Initialize Firebase
    const config = {
        apiKey: "AIzaSyDqGfttOXFDQTBnu0nfim29Mk4zu2VV4N0",
        authDomain: "salata-56485.firebaseapp.com",
        projectId: "salata-56485",
        storageBucket: "salata-56485.appspot.com",
        messagingSenderId: "1064638521855",
        appId: "1:1064638521855:web:a79670af70d7d735c7c7ca",
        measurementId: "G-SVJZ5P4871"
    };
    const app = initializeApp(config);
    const firestore = getFirestore(app);
    const auth = getAuth(app);

    interface Restaurant {
        name?: string;
        description?: string;
        image?: string;
        id?: string;
    }

    const restaurants = collectionStore<Restaurant>(firestore, 'restaurants');

    const restaurantsStore = writable();
    $: restaurantsStore.set(restaurants);

    setContext('restaurants', restaurantsStore);
</script>

<FirebaseApp {auth} {firestore}>
    <SignedIn let:user let:signOut>
        <p>Hello {user.uid}</p>
      <Button on:click={signOut}>
        Çıkış yap
      </Button>
    </SignedIn>
    
    <SignedOut let:auth>
      <Button on:click={() => signInAnonymously(auth)} >
        Giriş yap
      </Button>
    </SignedOut>

    <div class="max-w-4xl">
        carousel here
    </div>
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3 max-w-7xl mx-auto my-10">

<Collection ref={'restaurants'} let:data>
        {#each data as restaurant}
        <div class="space-y-4">
            <Card img={restaurant.image}>
              <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{restaurant.name}</h5>
              <p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">{restaurant.description}</p>
              <Button href="/restaurants/{restaurant.id}">
                Göz at
              </Button>
            </Card>
        </div>
        {/each}
        </Collection>
      </div>
</FirebaseApp>

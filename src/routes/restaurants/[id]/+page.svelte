<script lang="ts">
    import { initializeApp } from 'firebase/app';
    import { getFirestore } from 'firebase/firestore';
    import { getAuth } from 'firebase/auth';
    import { Doc, FirebaseApp } from 'sveltefire';
    import { page } from '$app/stores';
    import { Card, Button } from 'flowbite-svelte';

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
</script>

<FirebaseApp {auth} {firestore}>
    <Doc ref={'restaurants/' + $page.params.id} let:data>
        <h1 class="mb-4 text-4xl font-bold leading-none tracking-tight text-gray-600 md:text-5xl lg:text-6x">{data.name}</h1>
        {#each data.foods as food}
        <div class="space-y-4">
            <Card img={food.image} href="/" horizontal size="md">
              <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{food.name}</h5>
            </Card>
          </div>
        {/each}
    </Doc>
</FirebaseApp>
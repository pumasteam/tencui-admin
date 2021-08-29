<script>
	import '../app.postcss';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import { isAuthenticated } from '$lib/store';
	import { onMount } from 'svelte';
	import auth from '$lib/authService';
	let auth0Client;
	onMount(async () => {
		auth0Client = await auth.createClient();

		isAuthenticated.set(await auth0Client.isAuthenticated());
		user.set(await auth0Client.getUser());
	});

	function login() {
		auth.loginWithPopup(auth0Client);
	}
</script>

<Header />
<main>
{#if !$isAuthenticated}

<div class="bg-white dark:bg-gray-800 ">
    <div class="text-center w-full mx-auto py-12 px-4 sm:px-6 lg:py-16 lg:px-8 z-20">
        <h2 class="text-3xl font-extrabold text-black dark:text-white sm:text-4xl">
            <span class="block">
                Llevamos la educación a los que no la tienen
            </span>
            <span class="block text-indigo-500">
                Construye educacion offline.
            </span>
        </h2>
        <p class="text-xl mt-4 max-w-md mx-auto text-gray-400">
            Muchos estudiantes tienen facilidades a la hora de tomar clases en linea, pero los demas se quedan sin estudiar
        </p>
        <div class="lg:mt-0 lg:flex-shrink-0">
            <div class="mt-12 inline-flex rounded-md shadow">
                <button on:click={login()} type="button" class="py-4 px-6  bg-indigo-600 hover:bg-indigo-700 focus:ring-indigo-500 focus:ring-offset-indigo-200 text-white w-full transition ease-in duration-200 text-center text-base font-semibold shadow-md focus:outline-none focus:ring-2 focus:ring-offset-2  rounded-lg ">
                    Inicia ya
                </button>
            </div>
        </div>
    </div>
</div>
{:else}
	<slot />
{/if}
</main>
<Footer />

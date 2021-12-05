<!-- JS -->
<script>
	import supabase from '$lib/db.js';
	import { page, session } from '$app/stores';
	import { browser } from '$app/env';
	import { goto } from '$app/navigation';
	import Navbar from '$lib/Navbar.svelte';
	// code that runs only in the browser
	if (browser) {
		$session = supabase.auth.session(); // set session
		redirect();

		supabase.auth.onAuthStateChange((userSession) => {
			$session = userSession; // set session
			redirect();
		});
	}
	function redirect() {
		//login redirect
		if ($session && $page.path === '/login') {
			goto('/');
		}
		//logout redirect
		if (!$session && $page.path === '/') {
			goto('/login');
		}
	}
</script>

<!-- HTML -->
<Navbar />
<slot />

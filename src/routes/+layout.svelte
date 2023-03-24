<script lang="ts">
	import '../app.postcss';
	import { onMount } from 'svelte';
	import {
		DarkMode,
		Navbar,
		NavBrand,
		NavLi,
		NavUl,
		NavHamburger,
	} from 'flowbite-svelte';



	let breakPoint: number = 1024;
	let width: number;
	let activateClickOutside = true;
	let drawerHidden: boolean = false;
	$: if (width >= breakPoint) {
		drawerHidden = false;
		activateClickOutside = false;
	} else {
		drawerHidden = true;
		activateClickOutside = true;
	}
	onMount(() => {
		if (width >= breakPoint) {
			drawerHidden = false;
			activateClickOutside = false;
		} else {
			drawerHidden = true;
			activateClickOutside = true;
		}
	});
	let darkmodebtn =
		'text-gray-500 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 rounded-lg text-lg p-2.5 fixed right-2 top-12  md:top-3 md:right-2 z-50';
	let divClass = 'w-full md:block md:w-auto';
	let ulClass =
		'flex flex-col p-4 text-center mt-4 md:flex-row md:space-x-8 md:mt-0 md:text-lg md:font-medium';
</script>

<svelte:window bind:innerWidth={width} />

<header class="sticky top-0 z-50">
	<Navbar let:hidden let:toggle style="z-index: 50; top: 0;">
		<DarkMode btnClass={darkmodebtn} />

		<NavBrand href="/" class="">
			<span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white pl-4">
				WikiSafari
			</span>
		</NavBrand>
		<NavHamburger on:click={toggle} />
		<NavUl {hidden} {divClass} {ulClass}>
			<NavLi href="/">Home</NavLi>
			<NavLi href="/pages/about">About</NavLi>
			<NavLi href="https://github.com/shinokada/flowbite-sveltekit-responsive-sidebar-layout"
				>GitHub</NavLi
			>
		</NavUl>
	</Navbar>
</header>


<main >
	<slot />
</main>

<script>
	import { onMount } from 'svelte';

	const menuItems = [
		{ label: 'How it works', href: '/how-it-works' },
		{ label: 'Benefits', href: '/benefits' },
		{ label: 'Features', href: '/candidates' },
		{ label: 'Pricing', href: '/pricing' },
		{ label: 'About', href: '/about' }
	];

	let isAtTop = true;
	let scrollY = 0;
	let isMenuOpen = false;

	$: isAtTop = scrollY === 0;

	const toggleMenu = () => {
		isMenuOpen = !isMenuOpen;
	};

	const closeMenu = () => {
		isMenuOpen = false;
	};

	onMount(() => {
		const handleResize = () => {
			if (window.innerWidth >= 1024) {
				closeMenu();
			}
		};

		window.addEventListener('resize', handleResize);

		return () => {
			window.removeEventListener('resize', handleResize);
		};
	});
</script>

<svelte:window bind:scrollY />
<header
	class="fixed inset-x-8 top-4 rounded-xl z-50 transition-all duration-300 ease-in-out"
	class:header-shadow={!isAtTop}
>
	<div class="container mx-auto px-4 py-4 flex flex-wrap items-center justify-between">
		<div class="flex items-center">
			<a href="/"> <span class="text-2xl font-bold text-white">ProConnect</span></a>
		</div>

		<nav class="hidden lg:flex space-x-8">
			{#each menuItems as item}
				<a
					href={item.href}
					class="text-neutral-200 hover:text-lime-500 uppercase font-medium transition-colors duration-300 ease-in-out relative group"
				>
					{item.label}
					<span
						class="absolute left-0 bottom-0 w-0 h-0.5 bg-lime-500 transition-all duration-300 ease-in-out group-hover:w-full"
					></span>
				</a>
			{/each}
		</nav>

		<div class="hidden lg:flex space-x-4">
			<div>
				<a href="/signin" class="btn link"> Log in </a>
				<a href="/signup" class="btn"> Sign Up </a>
			</div>
		</div>

		<button
			class="lg:hidden text-gray-600 hover:text-gray-600 focus:outline-none"
			on:click={toggleMenu}
			aria-label="Toggle menu"
		>
			<svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					d={isMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'}
				/>
			</svg>
		</button>
	</div>

	{#if isMenuOpen}
		<div class="lg:hidden menu-shadow rounded-xl">
			<nav class="px-4 pt-2 pb-4 space-y-2">
				{#each menuItems as item}
					<a
						href={item.href}
						class="block text-neutral-900 uppercase tracking-wide text-sm p-2 font-medium transition-colors duration-300 ease-in-out"
						on:click={closeMenu}
					>
						{item.label}
					</a>
				{/each}
			</nav>

			<div class="px-4 pt-2 pb-4 space-y-2">
				<a
					href="/signin"
					class="block text-neutral-900 uppercase tracking-wide text-sm p-2 font-medium transition-colors duration-300 ease-in-out"
					on:click={closeMenu}
				>
					Log in
				</a>
				<a
					href="/signup"
					class="block text-neutral-900 uppercase tracking-wide text-sm p-2 font-medium transition-colors duration-300 ease-in-out"
					on:click={closeMenu}
				>
					Sign Up
				</a>
			</div>
		</div>
	{/if}
</header>

<style lang="postcss">
	.header-shadow {
		@apply bg-white/5 backdrop-blur-sm shadow-lg;
	}
	.menu-shadow {
		@apply bg-white/80 backdrop-blur-sm shadow-lg;
	}
</style>

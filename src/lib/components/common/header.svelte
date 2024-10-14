<script>
	const menuItems = [
		{ label: 'How it works', href: '/how-it-works' },
		{ label: 'Benefits', href: '/benefits' },
		{ label: 'Features', href: '/candidates' },
		{ label: 'Pricing', href: '/pricing' },
		{ label: 'About', href: '/about' }
	];

	let isAtTop = true;
	let scrollY = 0;

	$: isAtTop = scrollY === 0;
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

		<button class="lg:hidden text-gray-600 hover:text-gray-600 focus:outline-none">
			<svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					d="M4 6h16M4 12h16M4 18h16"
				/>
			</svg>
		</button>
	</div>
</header>

<style lang="postcss">
	.header-shadow {
		@apply bg-white/5 backdrop-blur-sm shadow-lg;
	}
</style>

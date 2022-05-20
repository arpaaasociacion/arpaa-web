<script context="module">
	export async function load({ url }) {
		return {
			props: { url }
		};
	}
</script>

<script lang="ts">
	import 'verdu/fonts/circular.css';
	import 'verdu/fonts/operator.css';
	import Transition from '$lib/components/Transition.svelte';

	export let url: string;
</script>

<main>
	<Transition {url}>
		<slot />
	</Transition>
</main>

<style lang="scss">
	:global {
		@import '../routes/global';
		@import 'verdu/verdu.scss';
	}

	main {
		background: var(--bg);
		color: var(--base);
		transition: 200ms;
	}
</style>

<script lang="ts">
	import type { welcomeType } from '$lib/types';
	import { onMount } from 'svelte';

	export let data: welcomeType;
	const { title, message } = data;
	let wheelEl: HTMLElement;
	const months = [
		'January',
		'February',
		'March',
		'April',
		'May',
		'June',
		'July',
		'August',
		'September',
		'October',
		'November',
		'December'
	];

	let inc = 360 / 12;
	let move = 0;

	function next() {
		move -= inc;
		wheelEl.style.transform = `rotate(${move}deg)`;
	}

	function prev() {
		move += inc;
		wheelEl.style.transform = `rotate(${move}deg)`;
	}

	onMount(() => {
		const itemsEl = document.querySelectorAll('.item');
		const X = 'translateX(-50%)';

		itemsEl.forEach((el: HTMLElement, i) => {
			el.style.transform = `${X} rotateZ(${inc * i}deg)`;
		});
	});
</script>

<svelte:head>
	<title>{title}</title>
</svelte:head>

<div class="wrapper row jcenter aend fill">
	<ul class="wheel" bind:this={wheelEl}>
		{#each months as month}
			<li class="item row jcenter">
				<span class="row fcenter">{month.substring(0, 3)}</span>
			</li>
		{/each}
	</ul>

	<div class="row buttons">
		<button class="pri semi" on:click={prev}>ANTERIOR</button>
		<button class="pri semi" on:click={next}>SIGUIENTE</button>
	</div>
</div>

<style lang="scss">
	.wheel {
		position: absolute;
		top: -40%;
		width: 120vw;
		min-width: 120vw;
		height: 120vw;
		min-height: 120vw;
		background: $pri;
		border-radius: 50%;
		color: $white;
		transition: 1s ease-in-out;
		margin-bottom: 100px;

		.item {
			position: absolute;
			top: 0;
			left: 50%;
			width: 50px;
			height: 50%;
			transform-origin: bottom;

			span {
				width: 50px;
				height: 50px;
				background: $grey;
				border-radius: 50%;
				transform: rotate(180deg) translateY(50%) scale(1.5);
			}
		}
	}

	.buttons {
		gap: 20px;
		padding: 20px;

		button {
			color: $white;
		}
	}
</style>

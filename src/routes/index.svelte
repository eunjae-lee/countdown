<script lang="ts" context="module">
	export async function load({ url }) {
		return {
			props: {
				givenTimeStr: url.searchParams.get('time')
			}
		};
	}
</script>

<script lang="ts">
	import Countdown from '$lib/components/countdown.svelte';
	import { onMount } from 'svelte';

	export let givenTimeStr: string;
	let targetTimeStr: string;
	let targetTime: Date;

	function setTimeStr(timeStr: string) {
		if (!timeStr) {
			return;
		}
		const [hour, minute] = timeStr.split(':');
		const now = new Date();
		now.setHours(parseInt(hour, 10));
		now.setMinutes(parseInt(minute, 10));

		targetTime = now;
	}

	onMount(() => {
		if (givenTimeStr) {
			setTimeStr(givenTimeStr);
		}
	});
</script>

<div class="h-screen">
	<div class="flex flex-col gap-4 h-full items-center justify-center">
		{#if targetTime === undefined}
			<p class="text-lg font-bold">Enter countdown time:</p>
			<input bind:value={targetTimeStr} type="time" class="text-xl input input-bordered" />
			<button type="button" class="btn" on:click={() => setTimeStr(targetTimeStr)}>Show</button>
		{:else}
			<Countdown {targetTime} />
		{/if}
	</div>
</div>

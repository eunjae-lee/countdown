<script lang="ts">
	import { onDestroy, onMount } from 'svelte';

	export let targetTime: Date;

	let hours: number;
	let minutes: number;
	let seconds: number;

	let intervalId: any;

	onMount(() => {
		intervalId = setInterval(() => {
			let totalSeconds = (targetTime.getTime() - new Date().getTime()) / 1000;
			if (totalSeconds < 0) {
				totalSeconds = 0;
			}
			hours = Math.floor(totalSeconds / 60 / 60);

			totalSeconds = totalSeconds % (60 * 60);
			minutes = Math.floor(totalSeconds / 60);

			totalSeconds = totalSeconds % 60;
			seconds = totalSeconds;
		}, 1000);
	});

	onDestroy(() => {
		clearInterval(intervalId);
	});
</script>

<div class="grid grid-flow-col gap-5 text-center auto-cols-max">
	<div class="flex flex-col">
		<span class="countdown font-mono text-5xl">
			<span style={`--value:${hours};`} />
		</span>
		hours
	</div>
	<div class="flex flex-col">
		<span class="countdown font-mono text-5xl">
			<span style={`--value:${minutes};`} />
		</span>
		min
	</div>
	<div class="flex flex-col">
		<span class="countdown font-mono text-5xl">
			<span style={`--value:${seconds};`} />
		</span>
		sec
	</div>
</div>

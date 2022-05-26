<script lang="ts">
	let targetTimeStr: string;
</script>

<div class="h-screen">
	<div class="flex flex-col gap-4 h-full items-center justify-center">
		<p class="text-lg font-bold">Enter countdown time:</p>
		<input bind:value={targetTimeStr} type="time" class="text-xl input input-bordered" />
		<a sveltekit:prefetch href={`${targetTimeStr}`} class="btn">Show</a>
	</div>
</div>

<script lang="ts" context="module">
	function parseTimeStr(timeStr: string) {
		if (!timeStr) {
			return null;
		}
		const [hour, minute] = timeStr.split(':');
		const date = new Date();
		date.setHours(parseInt(hour, 10));
		date.setMinutes(parseInt(minute, 10));

		return date;
	}

	export async function load({ params }) {
		return {
			props: {
				targetTime: parseTimeStr(params.slug)
			}
		};
	}
</script>

<script lang="ts">
	import Countdown from '$lib/components/countdown.svelte';

	export let targetTime: Date;
</script>

<div class="h-screen">
	<div class="flex flex-col gap-4 h-full items-center justify-center">
		<Countdown {targetTime} />
	</div>
</div>

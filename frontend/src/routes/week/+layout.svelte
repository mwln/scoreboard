<script lang="ts">
	import { type MatchupWeek } from '$lib';
	import { ArrowBigLeft, ArrowBigRight } from 'lucide-svelte';
	import { enhance } from '$app/forms';
	import { page } from '$app/stores';

	let selected_week: MatchupWeek | 'current' = $derived.by(() => {
		if ($page.params.id) {
			return Number($page.params.id) as MatchupWeek;
		} else {
			return 'current';
		}
	});
</script>

<div class="mt-4 flex w-full items-center justify-center">
	<div class="flex items-center gap-4 text-xl">
		<form method="POST" use:enhance action="/week?/decrement">
			<button name="decrement" id="increment" class="rounded-full border-2 border-secondary-300 p-1"
				><ArrowBigLeft class="stroke-secondary-300" /></button
			>
			<input hidden name="selected_week" id="selected_week" value={selected_week} />
		</form>
		<p>{'Week ' + selected_week}</p>
		<form method="POST" use:enhance action="/week?/increment">
			<button name="increment" id="increment" class="rounded-full border-2 border-secondary-300 p-1"
				><ArrowBigRight class="stroke-secondary-300" /></button
			>
			<input hidden name="selected_week" id="selected_week" value={selected_week} />
		</form>
	</div>
</div>

<!-- svelte-ignore slot_element_deprecated -->
<slot />

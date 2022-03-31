
<script>
	import { tweened } from 'svelte/motion';
	let orig = 2 * 60;
	let timer = tweened(orig);
	
	setInterval(() => {
		if ($timer > 0) $timer--;
	}, 1000);
	$: minut = Math.floor($timer / 60);
	$: sec = Math.floor($timer - minut * 60);
</script>

{#if minut == 0 && sec == 0}
	<div class="timer">
		<div class="modal">
			<h3>Test Time is Over</h3>
			<a href="/resultPage"><button>See Your Result</button></a>
		</div>
	</div>
{:else}
	<span>{minut}:</span>
	<span>{sec}</span>
		
	
{/if}



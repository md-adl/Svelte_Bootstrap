<script>
	// @ts-nocheck

	import { fly } from 'svelte/transition';
	import Header from '../components/Header.svelte';
	import { post } from '../store';
	import { chooseAns } from '../store';
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	export let show = true;
	let postData = [];
	import { onMount } from 'svelte';
	onMount(() => {
		post.subscribe((value) => {
			postData = value;
		});
	});
	//     import {content_text} from 'data/jsonFile.json'\
	const setCorrectValue = (i) => {
		dispatch('changeIndex', i);
	};

	$: data = $chooseAns.filter(Boolean);
</script>

{#if show}
	<nav transition:fly={{ x: -550, opacity: 1 }} class="">
		<div
			class="list position-fixed  start-0 mh-100 bg-white text-dark border d-flex flex-column p-2"
			style="width:200px;top:58px"
		>
			<div class="mb-0">
				<p class="border m-0 p-1 list-group-item list-group-item-action ">attempted :{data.length}</p>
				<p class="border mt-1 p-1 list-group-item list-group-item-action ">unattempted : {11 - data.length}</p>
			</div>
				{#each postData as dataItem, i (dataItem)}
					<span
						id="list{i}"
						class=" col-12 text-truncate  p-1 border list-group-item list-group-item-action "
						on:click={setCorrectValue(i)}
                        style="cursor: pointer;"
					>
						Q{i + 1}
						{JSON.parse(dataItem.content_text).question}
					</span>
				{/each}
		</div>
	</nav>
{/if}

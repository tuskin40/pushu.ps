<!--  
	The main call to action button that switches to next page
	Usage: <MainAction>Button label</MainAction>
-->



<script>

	// imports
	// ------------------------------------------------------------------------
	import { onMount } from 'svelte';
	import state from '../Data/state.js';
	import { appear } from '../Helpers/transitions.js';
	import { createEventDispatcher } from 'svelte';


	// properties
	// ------------------------------------------------------------------------
	// what page do you want to switch to
	export let changePageTo = null;
	// the delay after which the button will appear on the page
	export let delay = 400;
	// if the area for clicking should forced to small
	export let forceSmallClickArea = false;


	// local variables
	// ------------------------------------------------------------------------
	let dispatch = createEventDispatcher();


	// purpose:		performs the main action assigned to the button
	//				most likely changes the page or just dispatches an event
	// returns:		shows changed page, or dispatches an 'mainAction' event
	// ------------------------------------------------------------------------
	let action = () => {
		dispatch('mainAction');

		if(changePageTo) {
			state.setPage(changePageTo);
		}
	};

</script>

<style>

	.action-main {
		padding-top: .8em;

		text-align: left;
		text-transform: uppercase;
		line-height: 1.05em;
		font-size: 2.75rem;
		font-weight: 600;

		user-select: none;
	}

	.action-main:not(.action-main-small):only-of-type {
		padding-top: 18vh;
	}

	@media (min-height: 551px) and (max-height: 630px) {
		.action-main {
			font-size: 2rem;
		}
	}

</style>




<button
	in:appear="{ {from: 'bottom', delay: parseInt(delay)} }"
	type="button"
	class="action-main"
	class:action-main-small="{ forceSmallClickArea }"
	on:click="{ action }"
>
	<slot></slot>
</button>
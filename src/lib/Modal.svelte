<script lang="ts">
	import Cancel from './Cancel.svelte';
	import { fade, scale } from 'svelte/transition';

	export let open = false;
	export let includedTrigger = true;
	export let dismissible = true;
</script>

{#if includedTrigger}
	<button
		on:click={() => {
			open = !open;
		}}
	>
		<slot name="triggerLabel">Open Modal</slot>
	</button>
{/if}

{#if open}
	<div class="container">
		<div role="dialog" class="modal" in:scale out:fade>
			{#if dismissible}
				<button
					class="close-btn"
					aria-label="Close Modal or Dialog"
					on:click={() => {
						open = false;
					}}
				>
					<Cancel />
				</button>
			{/if}
			<slot />
			<div class="modal-actions">
				<slot name="modalActions" />
			</div>
		</div>
		<div
			class="overlay"
			transition:fade
			on:click={() => {
				if (dismissible) {
					open = false;
				}
			}}
		/>
	</div>
{/if}

<style>
	.container {
		isolation: isolate;
		position: absolute;
	}
	.modal {
		z-index: 1;
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		max-height: calc(100vh - 4em);
		width: fit-content;
		max-width: calc(100vw - 4em);
		overflow: auto;
		background: var(--as-modal-bg, white);
		padding: 1em;
		box-shadow: var(
			--as-modal-shadow,
			0 19px 38px rgba(0, 0, 0, 0.3),
			0 15px 12px rgba(0, 0, 0, 0.22)
		);
		border-radius: 0.25em;
	}
	.close-btn {
		float: right;
		padding: 0.2em;
		border-radius: 999999px;
	}
	.modal-actions {
		display: flex;
		justify-content: space-between;
		gap: 1em;
	}
	.overlay {
		z-index: -1;
		position: fixed;
		inset: 0;
		background: var(--as-modal-backdrop-bg, hsla(0, 0%, 0%, 0.8));
	}
</style>

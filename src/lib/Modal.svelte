<script lang="ts">
	import { fade, scale } from 'svelte/transition';
	import Cancel from './Cancel.svelte';

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
		<!-- Overlay / Backdrop -->
		<div
			class="overlay"
			transition:fade
			on:click={() => {
				if (dismissible) {
					open = false;
				}
			}}
		/>
		<!-- Modal -->
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
			<div class="modal-content">
				<slot />
				{#if $$slots.modalActions}
					<div class="modal-actions">
						<slot name="modalActions" />
					</div>
				{/if}
			</div>
		</div>
	</div>
{/if}

<style lang="">
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
		background: var(--as-modal-background, white);
		padding: 1em;
		box-shadow: var(
			--as-modal-shadow,
			0 19px 38px rgba(0, 0, 0, 0.3),
			0 15px 12px rgba(0, 0, 0, 0.22)
		);
		border-radius: var(--as-modal-border-radius, 0.25em);
	}
	:global(.modal-content > *:first-child) {
		margin-top: 0;
	}
	:global(.modal-content > *:last-child) {
		margin-bottom: 0;
	}
	.close-btn {
		float: right;
		aspect-ratio: 1/1;
		border-radius: 999999px;
		margin: 0;
	}
	.modal-actions {
		display: flex;
		justify-content: space-between;
		gap: 1em;
	}
	:global(.modal-actions > button) {
		flex-grow: 1;
	}
	.overlay {
		z-index: -1;
		position: fixed;
		inset: 0;
		background: var(--as-modal-backdrop-background, hsla(0, 0%, 0%, 0.8));
	}
</style>

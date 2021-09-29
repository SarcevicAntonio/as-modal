<script>
	import Modal from '$lib/Modal.svelte';

	let deleteModalOpen = false;

	function deleteEntry() {
		deleteModalOpen = false;
		alert('call delete function');
	}
</script>


<h2 id="demo">Demo</h2>

<section>
	<span>Some Entry in a List or something</span>

	<Modal bind:open={deleteModalOpen}>
		<svelte:fragment slot="triggerLabel">Delete</svelte:fragment>

		<h2>Are you sure you want to delete the entry?</h2>
		<p>This action can not be reversed.</p>

		<svelte:fragment slot="modalActions">
			<button on:click={() => (deleteModalOpen = false)}> No </button>
			<button on:click={deleteEntry}>Yes </button>
		</svelte:fragment>
	</Modal>
</section>

<style>
	span {
		margin-right: 1em;
	}
	h2 {
		margin-top: 0;
	}
	:global(button) {
		flex-grow: 1;
		display: inline-flex;
		justify-content: center;
		align-items: center;
		margin-bottom: 0;
		gap: 0.5em;
	}
</style>

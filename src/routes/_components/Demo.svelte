<script>
	import Modal from '$lib/Modal.svelte';

	let deleteModalOpen = false;

	function deleteEntry() {
		deleteModalOpen = false;
		alert('call delete function');
	}
</script>

<h2 id="demo">Demo</h2>

<h3>Quick Start (Super Simple)</h3>

<Modal>
	<h2>Hello World!</h2>
</Modal>

<h3>Delete Confirmation Dialog</h3>

<Modal bind:open={deleteModalOpen}>
	<svelte:fragment slot="triggerLabel">Delete</svelte:fragment>

	<h2>Are you sure you want to delete the entry?</h2>
	<p>This action can not be reversed.</p>

	<svelte:fragment slot="modalActions">
		<button on:click={() => (deleteModalOpen = false)}> No </button>
		<button on:click={deleteEntry}>Yes </button>
	</svelte:fragment>
</Modal>

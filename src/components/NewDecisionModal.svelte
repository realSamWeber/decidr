<script>
    export let closeModal;
    let options = [''];
    let question = '';

    function addOption() {
        options = [...options, ''];
    }

    function deleteOption(index) {
        options = options.filter((_, i) => i !== index);
    }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="fixed z-10 inset-0 overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true" on:click={closeModal}>
    <div class="flex items-center justify-center min-h-screen">
        <div class="bg-white rounded-lg text-left shadow-xl max-w-md w-full mx-auto p-4" on:click|stopPropagation>
            <h2 class="text-2xl font-bold mb-4">Create a New Room</h2>
            <input bind:value={question} placeholder="Enter question" class="p-2 w-full border rounded mb-2"/>
            {#each options as option, index (index)}
                <div class="flex justify-between items-center mb-2">
                    <input bind:value={options[index]} placeholder="Enter option" class="p-2 w-full border rounded"/>
                    <button class="bg-red-500 text-white py-1 px-2 rounded ml-2" on:click={() => deleteOption(index)}>Delete</button>
                </div>
            {/each}
            <button class="bg-blue-500 text-white py-2 px-4 rounded mb-4 w-full" on:click={addOption}>Add Option</button>
            <button class="bg-green-700 text-white py-2 px-4 rounded w-full" on:click={closeModal}>Submit</button>
        </div>
    </div>
</div>
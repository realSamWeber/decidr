<script>
	import { goto } from "$app/navigation";
    import NewDecisionModal from "../components/NewDecisionModal.svelte";

    let decision_code = '';
    let showModal = false;

    function createDecision() {
        showModal = true;
    }

    function closeModal() {
        showModal = false;
    }

    function handleKeydown(event) {
        if(event.key === 'Escape') {
            console.log("keydown")
            closeModal();
        }
    }

    // Reactive statement for showModal
    $: {
        if (typeof window !== "undefined") {
            if (showModal) {
                window.addEventListener('keydown', handleKeydown);
            } else {
                window.removeEventListener('keydown', handleKeydown);
            }
        }
    }

    async function joinDecision() {
        if(decision_code) {
            await goto(`/${decision_code}`);
            console.log('Joining decision with code: ', decision_code);
        } else {
            alert('Please enter a decision code');
        }
    }
</script>

<button type="button" class="btn variant-filled" on:click={createDecision}>New Decision</button>
<p>OR</p>
<p>Vote on an existing decision:</p>
<input bind:value={decision_code} placeholder="Enter code" class="input p-4"/>
<button type="button" class="btn variant-filled" on:click={joinDecision}>Join</button>

{#if showModal}
    <NewDecisionModal closeModal={closeModal}/>
{/if}
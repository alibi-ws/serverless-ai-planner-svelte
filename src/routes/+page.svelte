<!-- src/routes/+page.svelte -->
<script>
    // Change from $state() to regular let declarations
    let input = '';
    let result = '';
    let loading = false;
    
    async function handleSubmit() {
        if (!input.trim()) return;
        loading = true;
        try {
            const response = await fetch(`https://worker-ai-planner.alireza78-bk.workers.dev/?jobId=${encodeURIComponent(input)}`, {
                method: 'GET',
                headers: {
                    'Accept': 'application/json'
                }
            });
            if (!response.ok) {
                const errorText = await response.text();
                throw new Error(errorText);
            }
            const { status, itinerary } = await response.json();
            // Handle the response properly
			if (status === 'completed' && Array.isArray(itinerary) && itinerary.length > 0){
				result = `Status: ${status}\n\nItinerary:\n${JSON.stringify(itinerary, null, 2)}`;
			} else {
				result = `Status: ${status}`;
			}            
			
            // Force reactivity (just in case)
            result = result;
			} catch (error) {
            result = `Error: ${error.message}`;
        } finally {
            loading = false;
        }
    }
</script>

<div>
	<h1>Check status and Itinerary</h1>
	<input 
		type="text" 
		placeholder="Enter something..." 
		bind:value={input}
	/>
	<button onclick={handleSubmit} disabled={loading}>
		{loading ? 'Processing...' : 'Submit'}
	</button>
	
	{#if result}
		<div class="result">{result}</div>
	{/if}
</div>

<style>
	div { padding: 20px; font-family: Arial; }
	input { padding: 8px; margin-right: 8px; }
	button { padding: 8px 16px; }
	.result { 
		margin-top: 20px; 
		padding: 10px; 
		background: #f0f0f0; 
		border-radius: 4px; 
	}
</style>
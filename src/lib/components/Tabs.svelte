<script>
	let { tabs, activeTab, onTabChange } = $props();
</script>

<div class="tabs-container">
	{#each tabs as tab (tab.id)}
		<button
			onclick={() => onTabChange(tab.id)}
			class="tab-button"
			class:active={activeTab === tab.id}
		>
			{tab.label}
		</button>
	{/each}
</div>

<style>
	.tabs-container {
		display: flex;
		gap: 1rem;
		border-bottom: 2px solid #ccc;
		margin-bottom: 1.5rem;
	}
	.tab-button {
		padding: 0.5rem 1rem;
		border: none;
		background: none;
		font-size: 1rem;
		cursor: pointer;
		color: #555;
	}
	.tab-button.active {
		color: #000;
		font-weight: bold;
		border-bottom: 2px solid #000;
		/* Margen negativo para que la línea negra tape la línea gris del contenedor */
		margin-bottom: -2px;
	}
	.tab-button:hover:not(.active) {
		color: #333;
	}
</style>

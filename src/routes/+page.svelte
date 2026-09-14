<script>
	import Tabs from '$lib/components/Tabs.svelte';
	import { initialSedes } from '$lib/data/mockData.js';

	let activeTab = $state('sedes');
	const tabsConfig = [
		{
			id: 'equipos',
			label: 'Equipos'
		},
		{
			id: 'sedes',
			label: 'Sedes'
		},
		{
			id: 'cronograma',
			label: 'Cronograma'
		}
	];
</script>

<Tabs tabs={tabsConfig} {activeTab} onTabChange={(id) => (activeTab = id)} />

{#if activeTab === 'equipos'}
	<h2>Pestaña en construcción pa (equipos)</h2>
{:else if activeTab === 'cronograma'}
	<h2>Pestaña en construcción pa (cronograma)</h2>
{:else if activeTab === 'sedes'}
	<h2>Pestaña en construcción pa (sedes)</h2>
{/if}

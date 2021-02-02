<script context="module">

    import requests from '../data/requests.js';
    export async function preload() {
        try {
            const usStats = await requests.usStats();
            const historic = await requests.historicUs();
            return {usStats, historic};
        } catch(e) {
            this.error(500, "There was an error calling this api, please try again later.");
            return;
        }

    }
</script>

<script>
    import CovidStat from '../components/CovidStat.svelte';
    import CovidChart from '../components/CovidChart.svelte';
    import TableContainer from '../components/TableContainer.svelte';
    import About from './about.svelte';
    export let usStats;
    export let historic;
</script>

<svelte:head> 
    <title>
        Covid 19 Tracker
    </title>
</svelte:head>

<div class="section header">
    <div class="container">
        <h1>Covid 19 - US</h1>
    </div>
</div>

<CovidStat  {...usStats} />

<CovidChart historicData={historic} title="Covid-19" />

<TableContainer />
	




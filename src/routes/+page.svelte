<script>
    import YamlTextarea from "$lib/YamlTextarea.svelte";
    import Workflow from "$lib/Workflow.svelte";

    let yamlTextarea = $state();
    let workflow = $derived(yamlTextarea && yamlTextarea.getWorkflow());
</script>

<h1>GitHub Actions Workflow Visualizer</h1>

<YamlTextarea bind:this={yamlTextarea} />

<Workflow {workflow} />

<style>
    @import url("https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300..800;1,300..800&display=swap");

    :global {
        * {
            font-family: "Open Sans", Arial, sans-serif;
        }
    }
</style>

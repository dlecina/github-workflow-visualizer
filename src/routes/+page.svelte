<script>
    import YamlTextarea from "$lib/YamlTextarea.svelte";
    import Workflow from "$lib/Workflow.svelte";

    let yamlTextarea = $state();
    let workflow = $derived(yamlTextarea && yamlTextarea.getWorkflow());
</script>

<h1>GitHub Actions Workflow Diagram Maker</h1>

<YamlTextarea bind:this={yamlTextarea} />

<Workflow {workflow} />

<style>
    :global {
        * {
            font-family: Aptos, Arial, sans-serif;
        }
    }
</style>

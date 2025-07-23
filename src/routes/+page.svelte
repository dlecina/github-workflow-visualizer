<script>
    import YamlTextarea from "$lib/YamlTextarea.svelte";
    import Workflow from "$lib/Workflow.svelte";
    import Options from "$lib/Options.svelte";

    let yamlTextarea = $state();
    let optionsComponent = $state();

    let workflow = $derived(yamlTextarea && yamlTextarea.getWorkflow());
    let options = $derived(optionsComponent && optionsComponent.getOptions());
</script>

<div class="m-4">
    <h1 class="prose text-4xl mb-4">GitHub Actions Workflow Visualizer</h1>

    <YamlTextarea bind:this={yamlTextarea} />

    <hr class="mt-4 mb-4" />

    <Options bind:this={optionsComponent} />

    <hr class="mt-4 mb-4" />

    <Workflow {workflow} {options} />
</div>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300..800;1,300..800&display=swap");

    :global {
        * {
            font-family: "Open Sans", Arial, sans-serif;
        }

        hr {
            color: darkgrey;
        }
    }
</style>

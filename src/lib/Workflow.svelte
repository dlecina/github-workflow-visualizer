<script>
    import Job from "./Job.svelte";
    import Step from "./Step.svelte";
    import Legend from "./Legend.svelte";

    let { workflow = {}, showLegend = true, options = {} } = $props();

    let jobs = $derived(workflow.jobs || null);
</script>

{#if jobs}
    <div class="grid">
        {#if options.firstStep}
            <div class="beforeWorkflow">
                <Step step={options.firstStep} first></Step>
            </div>
        {/if}
        <div class="workflow">
            {#each Object.entries(jobs) as [name, job]}
                <Job {name} {job} />
            {/each}
            {#if showLegend}
                <Legend />
            {/if}
        </div>
        {#if options.lastStep}
            <div class="afterWorkflow">
                <Step step={options.lastStep} last></Step>
            </div>
        {/if}
    </div>
{/if}

<style>
    .grid {
        display: flex;
        align-items: center;
        justify-items: center;
        justify-self: center;
        max-width: 1200px;
    }

    .workflow {
        grid-column: 2;
        flex-grow: 1;
    }

    .beforeWorkflow,
    .afterWorkflow {
        flex-grow: 0;
        min-width: 150px;
        padding: 1em;
    }

    .beforeWorkflow {
        grid-column: 1;
    }

    .afterWorkflow {
        grid-column: 3;
    }
</style>

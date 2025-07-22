<script>
    import Job from "$lib/Job.svelte";
    import Step from "./Step.svelte";

    import github_logo from "$lib/assets/github.png";

    const codeCommitStep = {
        name: "Code Commit",
    };

    const deploymentStep = {
        name: "Deployment",
    };

    let { workflow = {} } = $props();
    let jobs = $derived(workflow.jobs || null);
</script>

{#if jobs}
    <div class="grid">
        <div class="beforeWorkflow">
            <Step step={codeCommitStep}></Step>
            <img alt="GitHub logo" src={github_logo} class="github_logo" />
        </div>
        <div class="workflow">
            {#each Object.entries(jobs) as [name, job]}
                <Job {name} {job} />
            {/each}
        </div>
        <div class="afterWorkflow">
            <Step step={deploymentStep}></Step>
        </div>
    </div>
{/if}

<style>
    .grid {
        display: flex;
        align-items: center;
        justify-items: center;
        max-width: 1200px;
    }

    .workflow {
        grid-column: 2;
        flex-grow: 1;
    }

    .beforeWorkflow,
    .afterWorkflow {
        flex-grow: 0;
        min-width: 130px;
        padding: 1em;
    }

    .beforeWorkflow {
        grid-column: 1;
    }

    .afterWorkflow {
        grid-column: 3;
    }

    .github_logo {
        display: block;
        margin: 0.3em auto;
        height: 1.2em;
    }
</style>

<script>
    import Step from "./Step.svelte";

    import github_actions_logo from "$lib/assets/github-actions.png";

    let { job = {}, name = "", showCondition = true } = $props();

    let optional = $derived(showCondition && job.if && !job.if.includes("always()"));
</script>

<div class={["job", { optional }]}>
    {#if optional}
        <p class="if">if {job.if}</p>
    {/if}

    <div class="github_actions_logo_container">
        <img alt="GitHub Actions logo" src={github_actions_logo} class="github_actions_logo" />
    </div>

    <h3 class="text-xl mt-2 mb-4">{name}</h3>

    <ol id="steps" class="mb-2">
        {#each job.steps as step, index}
            <Step {step} {index} />
        {/each}
    </ol>

    {#if job.uses}
        <p class="uses text-xs mb-2">📄 {job.uses}</p>
    {/if}
</div>

<style>
    .job {
        border: 1px solid darkgrey;
        padding: 0 1em;
        margin: 1em 0;
    }

    .optional {
        border: 1px dashed darkgrey;
    }

    h3 {
        text-align: center;
    }

    ol {
        padding-inline-start: 0;
    }

    .uses {
        text-align: center;
    }

    .github_actions_logo_container {
        position: relative;
    }

    .github_actions_logo {
        position: absolute;
        top: 0.8em;
        height: 1.2em;
    }

    .optional .github_actions_logo {
        top: 0;
    }

    .if {
        font-size: 0.6em;
        margin: 1em 0 1.1em 0;
    }
</style>

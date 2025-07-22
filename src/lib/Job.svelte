<script>
    import Step from "$lib/Step.svelte";

    import github_actions_logo from "$lib/assets/github-actions.png";

    let { job = {}, name = "" } = $props();
</script>

<div class="job">
    <div class="github_actions_logo_container">
        <img alt="GitHub Actions logo" src={github_actions_logo} class="github_actions_logo" />
    </div>

    <h3>{name}</h3>

    <ol id="steps">
        {#each job.steps as step, index}
            <Step {step} {index} />
        {/each}
    </ol>

    {#if job.uses}
        <p class="uses">📄 {job.uses}</p>
    {/if}
</div>

<style>
    .job {
        border: 1px solid darkgrey;
        padding: 0 1em;
        margin: 1em 0;
    }

    h3 {
        text-align: center;
        margin-block-start: 0.5em;
    }

    ol {
        padding-inline-start: 0;
    }

    .uses {
        font-size: 0.8em;
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
</style>

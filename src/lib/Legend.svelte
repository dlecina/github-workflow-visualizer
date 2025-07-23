<script>
    import { colors } from "./colors.svelte";

    let color_legend = {
        "Version Control": colors.git,
        "CI/CD": colors.default,
        "Static Code Analysis": colors.sonar,
        "Security Analysis": colors.security,
        Testing: colors.test,
        "Artifact Repository": colors.publish,
        "AWS Activity": colors.aws,
        Deployment: colors.deployment,
    };
</script>

<hr />
<div class="legend text-xs italic mt-2">
    <p class="mt-1 mr-2">Legend:</p>
    <ul class="mt-1">
        {#each Object.entries(color_legend) as [name, color]}
            <li><span class="rectangle" style="--c: {color}"></span>{name}</li>
        {/each}
    </ul>
</div>

<style>
    .legend {
        display: flex;
        justify-self: right;
    }

    hr {
        width: 54%;
        justify-self: right;
        border-style: dashed;
    }

    ul {
        column-count: 3;
        list-style-type: none;
    }

    .rectangle {
        display: inline-block;
        height: 0.9em;
        width: 1.5em;
        margin-right: 0.5em;
        background-color: var(--c);
    }
</style>

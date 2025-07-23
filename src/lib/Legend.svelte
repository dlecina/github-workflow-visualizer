<script>
    import { colors } from "./colors.svelte";

    let color_legend = {
        "Version Control": colors.git,
        "CI/CD": colors.default,
        "Static Code Analysis": colors.sonar,
        "Security Analysis": colors.security,
        Testing: colors.test,
        "Artifact Publication": colors.publish,
        "AWS Activity": colors.aws,
        Deployment: colors.deployment,
    };
</script>

<hr />
<div class="container">
    <h4>Legend:</h4>
    <ul>
        {#each Object.entries(color_legend) as [name, color]}
            <li><span class="rectangle" style="--c: {color}"></span>{name}</li>
        {/each}
    </ul>
</div>

<style>
    .container {
        display: flex;
        justify-self: right;
        font-size: 0.7em;
    }

    h4 {
        margin-top: 1em;
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

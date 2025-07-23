<script>
    let { step, index = null, showCondition = true } = $props();

    let condition = $derived.by(() => {
        let i = step.if;
        if (i) {
            // GitHub expression brackets
            i = i.replaceAll("${{", "");
            i = i.replaceAll("}}", "");

            // Truthy
            i = i.replaceAll(/!= ''/gi, "");
            i = i.replaceAll(/!= 'null'/gi, "");
            i = i.replaceAll(/== 'true'/gi, "");

            // Remove repetition (multiple truthy conditions)
            i = i.replaceAll(/s*(.+?)(?:s*&&\1)+/g, "");

            // Trim
            i.trim();
        }
        return i;
    });
    let optional = $derived(showCondition && condition && !condition.includes("always()"));

    const colors = {
        git: "#212121",
        sonar: "#1E88E5",
        security: "#8e44ad",
        test: "#00796B",
        publish: "#388E3C",
        deployment: "#c0392b",
        aws: "#FF9900",
        default: "#1A237E",
    };

    const colors_by_keyword = new Map(
        Object.entries({
            Commit: colors.git,
            Git: colors.git,
            Checkout: colors.git,
            Sonar: colors.sonar,
            Security: colors.security,
            Test: colors.test,
            Coverage: colors.test,
            Publish: colors.publish,
            JFrog: colors.publish,
            AWS: colors.aws,
            S3: colors.aws,
            Deployment: colors.deployment,
        }),
    );

    let color = $derived.by(() => {
        let key = colors_by_keyword.keys().find((key) => {
            let name = step.name || step.uses;
            return name?.toLowerCase().includes(key.toLowerCase());
        });
        if (key) {
            return colors_by_keyword.get(key);
        }
        return colors.default;
    });
</script>

<div class={["container", { optional }]}>
    {#if optional}
        <p class="if">if {condition}</p>
    {/if}
    <li style="--c: {color}">
        {#if index != null}
            <div class="indexCircle">
                <span class="index">{index + 1}</span>
            </div>
        {/if}
        {step.name || step.uses}
    </li>
</div>

<style>
    .container {
        display: inline-block;
        padding: 0.4em 0;
        margin-left: 4px;
        margin-right: 8px;
    }

    .optional {
        border: 1px dashed darkgray;
        margin-top: 4px;
        margin-bottom: 4px;
        padding-left: 0.6em;
        padding-right: 0.6em;
    }

    li {
        position: relative;
        display: inline-block;
        font-size: 0.8em;
        padding: 10px 10px 10px 20px;
        color: white;
        background-color: var(--c);
    }

    .optional li {
        margin-right: 0.4em;
    }

    li:before {
        content: "";
        position: absolute;
        width: 0;
        height: 0;
        left: 0;
        margin: -10px 0px 0 0px;
        border-top: 1.1rem solid transparent;
        border-left: 10px solid white;
        border-bottom: 1.1rem solid transparent;
    }

    li:after {
        content: "";
        position: absolute;
        width: 0;
        height: 0;
        margin: -10px 90px 0 10px;
        border-top: 1.1rem solid transparent;
        border-left: 10px solid var(--c);
        border-bottom: 1.1rem solid transparent;
    }

    .indexCircle {
        position: absolute;
        left: -12px;
        top: -8px;
        display: inline-block;
        z-index: 1;
        font-size: 0.7em;
        width: 1.2rem;
        height: 1.2rem;
        margin-left: 5px;
        background-color: var(--c);
        border-radius: 50%;
        border: 1px solid white;
    }

    .index {
        display: flex;
        color: white;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
    }

    .if {
        font-size: 0.6em;
        margin: 0 0 1.1em 0;
    }
</style>

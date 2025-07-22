<script>
    import * as yaml from "js-yaml";

    import exampleYaml from "./example.yaml?raw";
    // import exampleYaml from "./datalake-module-library-main-branch.yml?raw";
    // import exampleYaml from "./golang-library-pull-request.yml?raw";

    let yamlstr = $state(exampleYaml);
    let workflow = $derived.by(() => {
        try {
            return yaml.load(yamlstr);
        } catch (e) {
            return e;
        }
    });

    export function getWorkflow() {
        return workflow;
    }
</script>

<div class="container-flex">
    <div class="column-flex">
        <h2>YAML</h2>
        <textarea bind:value={yamlstr} placeholder="Enter YAML here..."></textarea>
    </div>
    <div class="column-flex">
        <h2>JSON</h2>
        <textarea readonly value={JSON.stringify(workflow, null, 2)} placeholder="Converted JSON"></textarea>
    </div>
</div>

<style>
    textarea {
        width: 100%;
        height: 400px;
        font-family: monospace;
        resize: vertical;
        background: #212121;
        color: #f1f1f1;
        border: 1px solid #444;
    }

    .container-flex {
        display: flex;
        gap: 20px;
    }

    .column-flex {
        flex: 1; /* Each column takes up equal available space */
        padding: 15px;
        background-color: #f0f0f0;
        border-radius: 5px;
    }

    @media (max-width: 800px) {
        .container-flex {
            flex-direction: column; /* Stacks columns vertically on smaller screens */
        }
    }
</style>

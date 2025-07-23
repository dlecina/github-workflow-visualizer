<script>
    let firstStep = $state("Code Commit");
    let lastStep = $state("Deployment");

    let options = $derived.by(() => {
        return {
            firstStep: firstStep && {
                name: firstStep,
            },
            lastStep: lastStep && {
                name: lastStep,
            },
        };
    });

    export function getOptions() {
        return options;
    }
</script>

<form>
    <h2 class="prose text-xl mb-4">Options</h2>

    <h3 class="prose text-l mb-2">Steps outside workflow</h3>
    <div class="flex flex-wrap -mx-3 mb-2">
        <div class="w-full md:w-1/8 px-3 mb-6 md:mb-0">
            <label class="block uppercase tracking-wide text-gray-700 text-sm font-bold mb-2" for="firstStep"> Before Workflow </label>
            <input
                type="text"
                id="firstStep"
                class="bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                placeholder="Step name"
                bind:value={firstStep}
            />
        </div>
        <div class="w-full md:w-1/8 px-3 mb-6 md:mb-0">
            <label class="block uppercase tracking-wide text-gray-700 text-sm font-bold mb-2" for="lastStep"> After Workflow </label>
            <input
                type="text"
                id="lastStep"
                class="bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                placeholder="Step name"
                bind:value={lastStep}
            />
        </div>
    </div>
    <span class="prose text-xs text-gray-400">(Leave blank to remove the step)</span>
</form>

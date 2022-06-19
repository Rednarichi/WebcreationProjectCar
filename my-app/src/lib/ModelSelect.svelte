<script>
    export let selectedBrand
    export let selectedModel
    
    
    </script>
    
    <div class="mb-3 xl:w-96">
        <label class="text-white text-xl py-0 mt-2" for=selectedModel>Choose your model:</label>
        <select class="form-select appearance-none
        block
        w-full
        px-3
        py-1.5
        text-base
        font-normal
        text-gray-700
        bg-white bg-clip-padding bg-no-repeat
        border border-solid border-gray-300
        rounded
        transition
        ease-in-out
        m-0
        focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" aria-label="Default select example"
        bind:value={selectedModel}>
                {#each selectedBrand.cars as option}
            <option value={option}>
                        {option.text}
                    </option>
                {/each}
            </select>
    </div>
<script>
    export let selectedBrand
    export let selectedModel
    

    let carOptions = [
            { id: "Ferrari", text: `Ferrari`, cars: [
            { id: "a1", text: `Ferrari Portofino M` },
            { id: "a2", text: `F8 Tributo` },
            { id: "a3", text: `F8 Spider` },
            { id: "a4", text: `Ferrari Roma` },
        ] },
            { id: "Bugatti", text: `Bugatti`, cars:  [
            { id: "b1", text: `Chiron Super Sport` },
            { id: "b2", text: `Chiron Divo` }
        ]},
            { id: "Lamborghini", text: `Lamborghini`, cars: [
            { id: "c1", text: `Aventador LP 780` },
            { id: "c2", text: `HURACÁN EVO RWD SPYDER` },
            { id: "c3", text: `URUS` }
        ] },
            { id: "Audi", text: `Audi`, cars: [
            { id: "d1", text: `Audi RS 5 Coupé` },
            { id: "d2", text: `Audi SQ8` }
        ] }
        ];
    </script>
    <div class="mb-3 xl:w-96">
        <label class="text-white text-xl py-0 mt-2" for=selectedBrand>Choose your brand:</label>
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
        bind:value={selectedBrand} on:change={() => [selectedModel] = selectedBrand.cars}>
                {#each carOptions as option}
                    <option value={option}>
                        {option.text}
                    </option>
                {/each}
            </select>
    </div>
<script>
    import { Datepicker } from 'svelte-calendar';
    import Test_drive from '/src/lib/test_drive_car.jpg'; 
    import dayjs from 'dayjs';
    import BrandSelect from "$lib/BrandSelect.svelte"
    import ModelSelect from "$lib/ModelSelect.svelte"
    import { supabase } from '../supabase.js';


    let selectedBrand = { id: "Ferrari", text: `Ferrari`, cars: [
            { id: "a1", text: `Ferrari Portofino M` },
            { id: "a2", text: `F8 Tributo` },
            { id: "a3", text: `F8 Spider` },
            { id: "a4", text: `Ferrari Roma` },
        ] };
    let selectedModel ={ id: "a1", text: `Ferrari Portofino M` };

    const theme = {
                calendar: {
                width: "700px",
                maxWidth: "100vw",
                legend: {
                height: "45px"
                },
                shadow: "0px 10px 26px rgba(0, 0, 0, 0.25)",
                colors: {
                text: {
                    primary: "#eee",
                    highlight: "#fff"
                },
                background: {
                    primary: "#333",
                    highlight: "#1065CC",
                    hover: "#222"
                },
                border: "#222"
                },
                font: {
                regular: "1.5em",
                large: "37em"
                },
                grid: {
                disabledOpacity: ".5",
                outsiderOpacity: ".7"
                }
            }
            }; 
    const today = new Date();
	const tomorrow = dayjs().add(30, 'day').toDate();
    let nDate = today;
    let nDay ="";

    const availableMorning = async () => {const { data, error } = await supabase
        .from('test_Drive')
        .select('Day, Morning')
        .eq('Day', nDate)
        if(error){
            return console.error(error)
        }
        return data[1]
        }
    const availableAfternoon = async () => {const { data, error } = await supabase
        .from('test_Drive')
        .select('Day, Afternoon')
        .eq('Day', nDate)
        if(error){
            return console.error(error)
        }
        return data[2]
    }
    const availableEvening = async () => {const { data, error } = await supabase
        .from('test_Drive')
        .select('Day, Evening')
        .eq('Day', nDate)
        if(error){
            return console.error(error)
        }
        return data[3]
    }    

    let data_set =[]
    if (nDay === "Morning") {
      data_set = [nDate,false, true, true]  
    }else if (nDay === "Afternoon") {
        data_set = [nDate,true, false, true]
    } else if (nDay === "Evening"){
            data_set = [nDate,true, true, false]
    }
    
    
	let values = {
		Brand: "",
		Model: "",
        Date: "",
        Session: "",
	}

   
		
        const returnSubmit = async () => {
            values = {
		    Brand: selectedBrand,
		    Model: selectedModel,
            Date: nDate,
            Session: nDay,
	    }

        const { error } = await supabase
        .from('car_test_submit')
        .insert(values)
        }
    




</script>


<h1 class="text_xl text-white">Book your test drive ! </h1>
<form on:submit|preventDefault={returnSubmit}>
    <BrandSelect bind:selectedBrand bind:selectedModel></BrandSelect>
    <ModelSelect bind:selectedModel {selectedBrand}></ModelSelect>  

    <span class="text-white text-xl"> Choose your available date: </span><Datepicker  start={today} end={tomorrow} {theme} />
    <div class="mb-3 xl:w-96">
        <label class="text-white text-xl py-0 mt-2" for=nDay>Choose your available time slot:</label>
        <select bind:value={nDay} class="form-select appearance-none
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
          mt-2
          focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" aria-label="Default select example">
            {#if availableMorning}
            <option value="Morning">Morning</option>
            {/if}
            {#if availableAfternoon}
            <option value="Afternoon">Afternoon</option>
            {/if}
            {#if availableEvening}
            <option value="Evening">Evening</option>
            {/if}
        </select>
        <button type="submit" class="
                px-6
                py-2.5
                bg-blue-600
                text-white
                font-medium
                text-xs
                leading-tight
                uppercase
                rounded
                shadow-md
                hover:bg-blue-700 hover:shadow-lg
                focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0
                active:bg-blue-800 active:shadow-lg
                transition
                duration-150
                ease-in-out mt-2" >
            Submit
        </button>
      </div>
    </form>
    console.log(nDay)

<img class="w-full .bg" src={Test_drive} alt="Test Drive">

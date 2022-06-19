<script>

    import { TextInput, TextArea, Button, FormGroup, Form } from "carbon-components-svelte";
        import { createForm } from "svelte-forms-lib";

        import { supabase } from '../supabase';

let apiResult = null;

const { form, errors, handleChange, handleSubmit, isSubmitting, handleReset } = createForm({
initialValues: { name: "", email: "", message: "" },
onSubmit: async values => {

    try {
        var result = await supabase.from("contact").insert(values);

        if (result.data != null) {
            apiResult = true;
        } else {
            apiResult = false;
        }

    } catch (ex) {
        apiResult = false;
    }

    handleReset();
}
});

</script>
<div class="bg-gray-500 shadow-md px-5 ">

    <h2>Contact Us</h2>
    <p>Enter the details to get in touch with us. You can remove your email at any time after this.</p> <br/><br/>

    <Form on:submit={handleSubmit}>

        <FormGroup>
            <TextInput labelText="Name" name="name" 
                on:change={handleChange} bind:value={$form.name}/>
        </FormGroup>

        <FormGroup>
            <TextInput labelText="Email" name="email" type="email" 
            on:change={handleChange} bind:value={$form.email}/>
        </FormGroup>


        <FormGroup>
            <TextArea labelText="Message" name="message" type="textarea"
            on:change={handleChange} bind:value={$form.message}/>
        </FormGroup>

        <Button type="submit" disabled={$isSubmitting}>Submit</Button>
    </Form>
</div>
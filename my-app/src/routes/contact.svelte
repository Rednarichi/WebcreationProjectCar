<script>

    import { TextInput, TextArea, Button, FormGroup, Form, InlineNotification } from "carbon-components-svelte";
        import { createForm } from "svelte-forms-lib";

    import { supabase } from '$lib/db';

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
<body class="bg-grey-400">
<div>

    <h2 class="text-white">Contact Us</h2>
    <p class="text-white">Enter the details to get in touch with us. You can remove your email at any time after this.</p> <br/><br/>

    {#if apiResult != null}

    {#if apiResult == true}
    <InlineNotification
        lowContrast
        kind="success"
        title="Success:"
        subtitle="Your message has been received"
    />
    {:else}
    <InlineNotification lowContrast kind="error"
        title="Error:"
        subtitle="An internal server error occurred."
    />

    {/if}    
    {/if}
    <Form on:submit={handleSubmit}>

        <FormGroup class="bg-slate-500">
            <TextInput labelText="Name" name="name" 
                on:change={handleChange} bind:value={$form.name}/>
        </FormGroup>

        <FormGroup class="bg-slate-500">
            <TextInput labelText="Email" name="email" type="email" 
            on:change={handleChange} bind:value={$form.email}/>
        </FormGroup>


        <FormGroup class="bg-slate-500">
            <TextArea labelText="Message" name="message" type="textarea"
            on:change={handleChange} bind:value={$form.message}/>
        </FormGroup>

        <Button class="bg-slate-500" type="submit" disabled={$isSubmitting}>Submit</Button>
    </Form>
</div>
</body>
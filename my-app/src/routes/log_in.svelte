<script>
    import {supabase} from "../supabase.js";
    import "../app.css";
    import Auth from "../Auth.svelte"
    import SignUp from "../Signup.svelte"
    console.log(supabase);
</script>

<div class="container mx-auto my-6 max-wl-g">
    <Auth/>
    <SignUp/>
    <slot></slot>
</div>
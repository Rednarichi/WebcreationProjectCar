<script>
	import { supabase } from "./supabase";

	let loading = false;
	let email, password;
	let message = { success: null, display: "" };

	const handleLogin = async () => {
		try {
			loading = true;
			const { error } = await supabase.auth.signIn({ email, password });
			if (error) throw error;
			message = { success: true, display: "Successfully logged in!" };
		} catch (error) {
			let errorMsg = error.error_description || error.message;
			message = { success: false, display: errorMsg };
		} finally {
			loading = false;
		}
	};
</script>

<form on:submit|preventDefault={handleLogin}>
	<div class="form-widget">
		<h1 class="text-2xl font-bold text-center text-white md:text-3xl">Login for users</h1>
		<p class="text-center text-white">Enter your email below to get a link to login</p>
		<div class="text-center text-white">
			<label for="email">Email Address</label>
			<input
				id='email' class="text-center text-black" type="email" placeholder="Your email"
				bind:value={email}
			/>
		</div>
		<div class="text-center text-white">
			<label for="password">Password</label>
			<input
				id='password' class="text-center text-black" type="password" placeholder="Set your new password"
				bind:value={password}
			/>
		</div>
		<div>
			<button
    type="submit"
    class="w-100px text-center shadow-sm rounded bg-blue-500 hover:bg-blue-600 text-white py-2 px-4">
    Log In
    </button>
		</div>
		{#if message.success != null}
			<div class="alert {message.success ? 'alert-success' : 'alert-danger'}" role="alert">
				{message.display}
			</div>
		{/if}
	</div>
</form>
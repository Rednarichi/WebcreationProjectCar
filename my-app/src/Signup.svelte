<script>
	import { supabase } from "./supabase";

	let loading = false;
	let email, password, confirmpassword;
	let message = { success: null, display: "" };

	const handleSignup = async () => {

		if (password != confirmpassword) {
			message = { success: false, display: "Password and Confirm Password fields do not match" };
			return;
		}

		try {
			loading = true;
			const { error } = await supabase.auth.signUp({ email, password });
			console.log(error);
			if (error) throw error;
			message = { success: true, display: "We have sent you an confirmation email. Please check your email" };
		} catch (error) {
			console.log(error);
			let errorMsg = error.error_description || error.message;
			message = { success: false, display: errorMsg };
		} finally {
			loading = false;
		}
	};
</script>

<form on:submit|preventDefault={handleSignup}>
	<div class="form-widget">
		<h1 class="text-2xl font-bold text-center text-white md:text-3xl">Signup form</h1>
		<p class="text-center text-white">Create an account and join the community of Auto Prestige</p>
		<div class="text-center text-white">
			<label for="email">Email address</label>
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
		<div class="text-center text-white">
			<label for="confirmpassword">Confirm Password</label>
			<input
				id='confirmpassword' class="text-center text-black" type="password" placeholder="Confirm your new password"
				bind:value={confirmpassword}
			/>
		</div>
		<div>
			<input type="submit" class="btn btn-success" value={loading ? "Loading" : "Sign up"}
				disabled={loading}
			/>
		</div>

		{#if message.success != null}
			<div class="alert {message.success ? 'alert-success' : 'alert-danger'}" role="alert">
				{message.display}
			</div>
		{/if}
	</div>
</form>
<script>
	import { supabase } from "./supabase";
	let loading = false;
	let email = ''; 
	let password = '';
	let confirmpassword ='';
	let message = { success: false, display: "" };
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
			// @ts-ignore
			let errorMsg = error.error_description || error.message;
			message = { success: false, display: errorMsg };
		} finally {
			loading = false;
		}
	};
</script>

<form
	on:submit|preventDefault={handleSignup}
>
	<div class="form-widget">
		<h1 class="text-center text-3xl text-gray-600">Create an account </h1>
		<p class = "text-center text-xl text-gray-600"> Join Auto Prestige community</p>


		<div class="form-group">
			<label for="email">Email address</label>
			<input
				id='email'
				class="form-control"
				type="email"
				placeholder="Your email"
				bind:value={email}
			/>
		</div>
		<div class="form-group">
			<label for="password">Password</label>
			<input
				id='password'
				class="form-control"
				type="password"
				placeholder="Set your new password"
				bind:value={password}
			/>
		</div>
		<div class="form-group">
			<label for="confirmpassword">Confirm Password</label>
			<input
				id='confirmpassword'
				class="form-control"
				type="password"
				placeholder="Confirm your new password"
				bind:value={confirmpassword}
			/>
		</div>
		<div>
			<button
			type="submit"
			class="w-full text-center shadow-sm rounded bg-blue-500 hover:bg-blue-600 text-white py-2 px-4">
			Sign Up
			</button>
		</div>
		{#if message.success != null}
			<div class="alert {message.success ? 'alert-success' : 'alert-danger'}" role="alert">
				{message.display}
			</div>
		{/if}
	</div>
</form>
<script>
// @ts-nocheck

	import { supabase } from "./supabase";
	let loading = false;
	let email = ''; 
	let password = '';
	let message = { success: false, display: "" };
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

<form
	on:submit|preventDefault={handleLogin}
>
	<div class="form-widget">
		<h1 class="text-center text-3xl text-gray-600 font-bold">Welcome to login portal</h1>
		<p class="text-center text-xl text-gray-600">Enter your email below to get a link to login</p>
		<div class="form-group">
			<label for="email">Email Address</label>
			<input
				id='email'
				class="form-group"
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
				placeholder="Input your password"
				bind:value={password}
			/>
		</div>
		<div>
			<button
			type="submit"
			class=" w-full mx-auto w-100px text-center shadow-sm rounded bg-blue-500 hover:bg-blue-600 text-white py-2 px-4">
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
<style>
	.form-widget {
		display: center;
		flex-direction: column;
		gap: 8px;
		background-color: #FEFFDE;
		padding: 2rem;
		border-radius: 0 0 8px 8px;
	}

</style>
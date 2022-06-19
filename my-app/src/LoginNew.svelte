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
		<h1 class="header">Welcome to Auto Prestige login portal</h1>
		<p class="description">Enter your email below to get a link to login</p>
		<div class="form-group">
			<label for="email">Email Address</label>
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
		<div>
			<input
				type="submit"
				class="btn btn-success"
				value={loading ? "Loading" : "Log in"}
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

<style>
	.form-widget {
		display: flex;
		flex-direction: column;
		gap: 10px;
		background-color: #FEFFDE;
		padding: 3rem;
		border-radius: 0 0 10px 10px;
	}
	.form-widget input[type="submit"] {
		width: 100%;
		margin-top: 1rem;
	}
</style>
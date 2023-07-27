<!-- src/routes/account/+page.svelte -->
<script lang="ts">
	import { enhance } from '$app/forms';
	import type { SubmitFunction } from '@sveltejs/kit';

	export let data;
	export let form;

	let { session, profile } = data;

	let profileForm: HTMLFormElement;
	let loading = false;
	let fullName = profile?.full_name ?? null;
	let username = profile?.username ?? null;
	let website = profile?.website ?? null;

	const handleSubmit: SubmitFunction = () => {
		loading = true;
		return async () => {
			loading = false;
		};
	};

	const handleSignOut: SubmitFunction = () => {
		loading = true;
		return async ({ update }) => {
			loading = false;
			update();
		};
	};
</script>

<div class="mx-auto container p-4">
	<h1 class="mb-4">Account Information</h1>
	<form
		id="account-info"
		method="post"
		action="?/update"
		use:enhance={handleSubmit}
		bind:this={profileForm}
	/>
	<form id="sign-out" method="post" action="?/signout" use:enhance={handleSignOut} />

	<label for="email" class="label">Email</label>
	<input
		id="email"
		form="account-info"
		type="text"
		class="input mb-4"
		value={session.user.email}
		disabled
	/>
	<label for="fullName" class="label">Full Name</label>
	<input
		id="fullName"
		form="account-info"
		name="fullName"
		type="text"
		class="input mb-4"
		value={form?.fullName ?? fullName}
	/>
	<label for="username" class="label">Username</label>
	<input
		id="username"
		form="account-info"
		name="username"
		type="text"
		class="input mb-4"
		value={form?.username ?? username}
	/>
	<label for="website" class="label">Website</label>
	<input
		id="website"
		form="account-info"
		name="website"
		type="url"
		class="input mb-4"
		value={form?.website ?? website}
	/>
	<div>
		<input
			type="submit"
			form="account-info"
			class="btn variant-filled-primary"
			value={loading ? 'Loading...' : 'Update'}
			disabled={loading}
		/>

		<button class="btn variant-filled-secondary ml-4" form="sign-out" disabled={loading}
			>Sign Out</button
		>
	</div>
</div>

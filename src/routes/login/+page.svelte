<!-- src/routes/+page.svelte -->
<script lang="ts">
	import { Auth } from '@supabase/auth-ui-svelte';
	import { ThemeMinimal } from '@supabase/auth-ui-shared';

	export let data;
</script>

<svelte:head>
	<title>User Management</title>
</svelte:head>

<div class="flex items-center justify-center">
	<Auth
		supabaseClient={data.supabase}
		view="magic_link"
		redirectTo={`${data.url}/auth/callback`}
		showLinks={false}
		additionalData={undefined}
		appearance={{ theme: ThemeMinimal, style: { input: 'color: #fff' } }}
	/>
</div>

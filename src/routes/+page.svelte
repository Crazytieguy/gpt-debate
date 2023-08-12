<script lang="ts">
  export let data;
  $: ({ supabase } = data);

  const handleSignIn = async () => {
    await supabase.auth.signInWithOAuth({
      provider: 'github',
      options: { redirectTo: `${location.origin}/auth/callback` }
    });
  };

  const handleSignOut = async () => {
    await supabase.auth.signOut();
  };
</script>

<p>
  Signed is as <strong>{data.session?.user.email}</strong>
</p>

<button type="button" class="btn variant-filled" on:click={handleSignIn}>Sign in</button>
<button type="button" class="btn variant-filled" on:click={handleSignOut}>Sign out</button>

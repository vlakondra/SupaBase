<script>
    import { supauser } from "./store";
</script>

<div class='m-8'>
    {#if $supauser.user}
            Привет {$supauser.user.email}!
    {/if}
    <p>
        ID: {$supauser.user.id}
    </p>
</div>
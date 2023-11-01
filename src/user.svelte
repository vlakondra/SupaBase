<script>
    import { supauser } from "./store";
</script>

<div class='m-8'>
    {#if $supauser.user}
            Привет {$supauser.user.email}
    {/if}
</div>
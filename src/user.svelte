<script>
    import { supauser } from "./store";
</script>
<div>
    {#if $supauser.user}
            Привет {$supauser.user.email}
    {/if}
</div>
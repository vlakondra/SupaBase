<script>
    import { supabase } from "./store";
	import {supauser} from "./store"
	import User from './user.svelte'

	import { onMount } from "svelte";
	export let name;
	let data 

	onMount(async () => {
		let n = await supabase
             .from('countries')
             .select('id,name')
			 console.log('N',n)
        data=n.data
	});


	async function signUpNewUser() {
  const { data, error } = await supabase.auth.signUp({
    email: 'kondrashkin.wladimir@yandex.ru',
    password: 'mazay123MAZAY',
    options: {
      redirectTo: {emailRedirectTo:'https://5173-vlakondra-supabase-7j950gy9dah.ws-eu105.gitpod.io/'}
    }
  })
  console.log(error, data.user.email)
  $supauser.user=data.user
}


async function signInUser() {

  const { data, error } = await supabase.auth.signInWithPassword({
    email: 'kondrashkin.wladimir@yandex.ru',
    password: 'mazay123MAZAY',
})

  console.log(error, data.user.email)
  $supauser.user=data.user

}
</script>

<main>
	<User/>
	<p>
		<button on:click={()=>signUpNewUser()}>SignUp</button>
	</p>
	<p>
		<button on:click={signInUser}>SignIn</button>
	</p>

{#if data}

{#each data  as item}
	 <div style='display:flex; flex-direction:row'>
		<p>{item.id}</p>
		<p>{item.name}</p>
	 </div>
{/each}
{/if}
</main>

<style>
	p{margin:10px}
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
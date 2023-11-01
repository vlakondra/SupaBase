<script>
    import { supabase } from "./store";
	import {supauser} from "./store"
	import User from './user.svelte'

	import { onMount } from "svelte";
	export let name;
	let data 

	import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte'


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

	
<div class="w-full max-w-sm p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700">
    <form class="space-y-6" action="#">
        <h5 class="text-xl font-medium text-gray-900 dark:text-white">Sign in to our platform</h5>
        <div>
            <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your email</label>
            <input type="email" name="email" id="email" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white" placeholder="name@company.com" required>
        </div>
        <div>
            <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your password</label>
            <input type="password" name="password" id="password" placeholder="••••••••" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white" required>
        </div>
        <div class="flex items-start">
            <div class="flex items-start">
                <div class="flex items-center h-5">
                    <input id="remember" type="checkbox" value="" class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800" required>
                </div>
                <label for="remember" class="ml-2 text-sm font-medium text-gray-900 dark:text-gray-300">Remember me</label>
            </div>
            <a href="#" class="ml-auto text-sm text-blue-700 hover:underline dark:text-blue-500">Lost Password?</a>
        </div>
        <button type="submit" class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Login to your account</button>
        <div class="text-sm font-medium text-gray-500 dark:text-gray-300">
            Not registered? <a href="#" class="text-blue-700 hover:underline dark:text-blue-500">Create account</a>
        </div>
    </form>
</div>


	<div class="mx-auto shadow-md ">
	<User/>
	<p>
		<button  class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 text-center mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
		   on:click={()=>signUpNewUser()}>SignUp</button>
	</p>
	<p>
		<button class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 shadow-lg shadow-blue-500/50 dark:shadow-lg dark:shadow-blue-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2 "
		 on:click={signInUser}>SignIn</button>
	</p>
</div>

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
		max-width: 1024px;
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
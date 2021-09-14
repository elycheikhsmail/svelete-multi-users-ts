<script lang="ts">
	import { apiBaseUrl } from '../../lib/api-url';
	let username = 'sidi';
	let password = '1234';
	let isLogin = false;

	function getData() {
		const data = JSON.stringify({ username, password });
		return data;
	}
	const show = async () => {
		const url = `${apiBaseUrl}/auth/register`; 
		const body = getData();
		const response = await fetch(url, {
			method: 'POST',
			credentials: "include",
			headers: {
				'Content-Type': 'application/json',
				'Access-Control-Allow-Origine': '*'
			},
			mode: 'cors',
			referrerPolicy: 'no-referrer',
			body
		});
	 
		  await response.text(); 
		//	window.location.assign('/');
	};

</script>

<main>
	<h1>inscription</h1>
 
	<div>
		<h1>Formulaire d'inscription </h1>
		<form>
			<p>
				<label for="username">username :</label>
				<input type="text" placeholder="username" bind:value={username} />
			</p>
			<p>
				<label for="password">mot de pass:</label>
				<input type="password" placeholder="Mot de passe" bind:value={password} />
			</p>
		</form>
		<p>
			<button on:click={show}> s'inscrire</button>
		</p>
	</div>
</main>

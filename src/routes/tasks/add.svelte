<script lang="ts">
	import { apiBaseUrl } from '../../lib/api-url';
	let text = 'sidi';

	function getData() {
		const data = JSON.stringify({ text });
		return data;
	}
	const show = async () => {
		const token = localStorage.getItem('accessToken') || ''; 
		const url = `${apiBaseUrl}/task` 
		const body = getData();
		const response = await fetch(url, {
			method: 'POST',
			credentials: "include",
			headers: {
				//'Access-Control-Allow-Headers':'true',
				'Content-Type': 'application/json',
				'Access-Control-Allow-Origine': `*`,
				//authorization: `bearer ${token}`
			},
			mode: 'cors',
			referrerPolicy: 'no-referrer',
			body
		});
		if (response.status == 200) {
			const responseJ = await response.json();
			console.log(responseJ);
			window.location.assign('/tasks');
		} else {
			localStorage.removeItem('accessToken');
		}
	};
</script>

<main>
	<div>
		<h1>Formulaire d'additon d une tache </h1>
		<form>
			<p>
				<label for="username"> task:</label>
				<input type="text" placeholder="username" bind:value={text} />
			</p>
		</form>
		<p>
			<button on:click={show}> show </button>
		</p>
	</div>
</main>

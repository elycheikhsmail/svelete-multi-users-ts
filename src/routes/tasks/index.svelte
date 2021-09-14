<script context="module" lang="ts">
	import { enhance } from '$lib/form';
	import type { Load } from '@sveltejs/kit';

	import { apiBaseUrl } from '../../lib/api-url';

	// see https://kit.svelte.dev/docs#loading
	export const load: Load = async ({fetch}) => {
		const url = `${apiBaseUrl}/task`;
		const res = await fetch(url, {
			credentials: 'include',
			headers: { 
				'Content-Type': 'application/json',
				'Access-Control-Allow-Origine': `*` 
			},
			mode: 'cors',
			referrerPolicy: 'no-referrer'
		});

		if (res.ok) {
			const todos = await res.json();

			return {
				props: { todos }
			};
		}

		const { message } = await res.json();

		return {
			error: new Error(message)
		};
	};
</script>

<script lang="ts">
	import { scale } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	type Task = {
		id: string;
		text: string;
	};

	export let todos: Task[]=[];
</script>

<svelte:head>
	<title>Todos</title>
</svelte:head>

<div >
	<h1>Todos</h1>
	{#each todos as todo (todo.id)}
		<div>
			{todo.text} <br>
             <button> remove</button>
             <button> edit</button>
            <hr>
		</div>
	{/each}
</div>

<style>
	.todos {
		width: 100%;
		max-width: var(--column-width);
		margin: var(--column-margin-top) auto 0 auto;
		line-height: 1;
	}

	.todo {
		display: grid;
		grid-template-columns: 2rem 1fr 2rem;
		grid-gap: 0.5rem;
		align-items: center;
		margin: 0 0 0.5rem 0;
		padding: 0.5rem;
		background-color: white;
		border-radius: 8px;
		filter: drop-shadow(2px 4px 6px rgba(0, 0, 0, 0.1));
		transform: translate(-1px, -1px);
		transition: filter 0.2s, transform 0.2s;
	}
</style>

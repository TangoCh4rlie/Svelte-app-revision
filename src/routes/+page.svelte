<script>
	import { createTodoStore } from './todos.js';
	import TodoList from './TodoList.svelte';

	const todos = createTodoStore([
		{ done: false, description: 'Réviser les mathématiques' }
	]);
</script>

<div class="board">
	<input
		placeholder="Quelle notion voulez-vous enregistrer"
		on:keydown={(e) => {
			if (e.key === 'Enter') {
				todos.add(e.currentTarget.value);
				e.currentTarget.value = '';
			}
		}}
	/>

    <h2>Liste des notions à traiter de la journée</h2>

	<div class="listes">
        <div class="todo">
            <h2>A faire</h2>
            <TodoList store={todos} done={false} />
        </div>
    
        <div class="done">
            <h2>Fait</h2>
            <TodoList store={todos} done={true} />
        </div>
    </div>
</div>

<style>
	.board {
		display: flex;
        flex-direction: column;
		max-width: 36em;
		margin: 0 auto;
        font-family: 'Courier New', Courier, monospace;
	}

    .listes {
        display: flex;
        flex-direction: row;
        border: solid;
    }

	.board > input {
		font-size: 1.4em;
		grid-column: 1/3;
		padding: 0.5em;
		margin: 0 0 1rem 0;
        font-family: 'Courier New', Courier, monospace;
	}

	h2 {
		font-size: 2em;
		font-weight: 200;
	}
</style>

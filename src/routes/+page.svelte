<script>
	import { createTodoStore } from './todos.js';
	import TodoList from './TodoList.svelte';

	const todos = createTodoStore([
		{ 
            done: false, description: 'Réviser les mathématiques' 
        }
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
        <div class="border border-black">
            <h2>A faire</h2>
            <TodoList store={todos} done={false} />
        </div>
    
        <div class="border border-black">
            <h2>Fait</h2>
            <TodoList store={todos} done={true} />
        </div>
    </div>
    {#if todos.length > 0}
        <!-- Insérez ici le code à afficher si la variable todos contient des éléments -->
    {:else}
        <button on:click={() => {todos.add("Ma première notion")}}>Ajouter votre première notion</button>
    {/if}
</div>

<style lang="postcss">
    :global(html) {
        background-color: theme(colors.gray.100);
    }

	.board {
		display: flex;
        flex-direction: column;
		max-width: 50em;
		margin: 0 auto;
        font-family: 'Courier New', Courier, monospace;
	}

    .listes {
        display: flex;
        flex-direction: row;
        border: solid;
    }

    .listes > * {
        flex-basis: 50%;
    }

	.board > input {
		font-size: 1.4em;
		grid-column: 1/3;
		padding: 0.5em;
		margin: 0 0 1rem 0;
        border-radius: 10px;
        border: solid;
        border-color: black;
        font-family: 'Courier New', Courier, monospace;
	}

	h2 {
		font-size: 2em;
		font-weight: 200;
	}
</style>

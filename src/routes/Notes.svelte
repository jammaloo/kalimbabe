<script lang="ts">
	export let notes = '';
	export let currentPosition = 0;

	let noteIndex = 0;
	const notesStruct = notes.split('\n').map((note) => {
		const noteLine = note.split(' ').map((n) => ({
			index: noteIndex++,
			note: n
		}));
		const startNoteIndex = noteLine[0]?.index || 0;
		const endNoteIndex = noteIndex;
		return {
			start: startNoteIndex,
			end: endNoteIndex,
			notes: noteLine,
		}
	});
	console.log('noteStruct', notesStruct);
	let maxIndex = noteIndex;
</script>


<div class="notes">
	{#each notesStruct as noteLine}
		<h1 class="noteLine {noteLine.start <= (currentPosition % maxIndex) && noteLine.end > (currentPosition % maxIndex) ? 'highlighted' : ''}">
			{#each noteLine.notes as note}
					<span class={`note ${(currentPosition % maxIndex) === note.index ? 'highlighted' : ''}`}>
						{note.note}
					</span>
			{/each}
		</h1>
	{/each}
</div>

<style>
	.notes {
		border-top: 1px solid rgba(0, 0, 0, 0.1);
		border-bottom: 1px solid rgba(0, 0, 0, 0.1);
		margin: 1rem 0;
		height: 100%;
		letter-spacing: 1rem;
	}

	.noteLine.highlighted {
		color: green;
	}

	.note.highlighted {
		color: red;
	}
</style>

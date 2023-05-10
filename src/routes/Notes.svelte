<script lang="ts">
	export let notes = '';
	export let currentPosition = 0;

	let noteIndex = 0;
	const notesStruct = notes.split('\n').map((note, lineIndex) => {
		const noteLine = note.split(' ').map((n) => ({
			index: noteIndex++,
			note: n
		}));
		const startNoteIndex = noteLine[0]?.index || 0;
		const endNoteIndex = noteIndex;
		return {
			index: lineIndex,
			start: startNoteIndex,
			end: endNoteIndex,
			notes: noteLine,
		}
	});
	$: currentPositionNormalized = currentPosition % noteIndex;
	$: currentLineIndex = notesStruct.find((noteLine) => noteLine.start <= currentPositionNormalized && noteLine.end > currentPositionNormalized).index;
</script>


<div class="notes">
	{#each notesStruct as noteLine}
		<h1
			class="noteLine"
			class:highlighted={noteLine.index === currentLineIndex}
		>
			{#each noteLine.notes as note}
					<span
						class="note"
						class:highlighted={currentPositionNormalized === note.index}
					>
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
	}

	.note {
		margin: 0 1rem;
	}

	.noteLine.highlighted {
		color: green;
	}

	.note.highlighted {
		color: red;
	}
</style>

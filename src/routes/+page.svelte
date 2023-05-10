<script>
	import Notes from './Notes.svelte';
	const notes = `
5
2 3 4
3 2 1
1 3 5
4 3 2
3 4 5
3
1 1
4 6 1′
7 6 5
3 5 4
3 2 2
3 4 5
3 1 1
`.trim();

let counter = 0;
setInterval?.(() => {
	counter++;
}, 1000);
</script>

<svelte:head>
	<title>Kalimba</title>
	<meta name="description" content="Kalimba" />
</svelte:head>

<section>
	<Notes notes={notes} currentPosition={counter} />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
</style>

<script>
	import Question from "./Question.svelte";
</script>

<style>
	h1, a {
		color: #3344ee
	}

	a {
		font-weight: 600;
		font-style: oblique;
		text-decoration: underline;
	}
</style>

<h1>Jeopardy!</h1>
<p>Using a simple <a target="_blank" href="https://github.com/rrosenlof/jeopardy-api">API</a> to return a random <i>Jeopardy!</i> clue that was used in an episode of the show.</p>
<hr />
<main>
	<Question />
</main>

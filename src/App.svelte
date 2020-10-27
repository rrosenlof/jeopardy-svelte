<script>
	import Question from "./Question.svelte";
</script>

<style type="text/scss">
	$color: #3344ee;

	h1, a {
		color: $color
	}

	a {
		font-weight: 600;
		font-style: oblique;
		text-decoration: underline;
	}
</style>

<h1><i>Jeopardy!</i> Clues</h1>
<p>Using a simple <a target="_blank" tabindex="-1" href="https://github.com/rrosenlof/jeopardy-api">API</a> to return a random <i>Jeopardy!</i> clue that was used in an episode of the show.</p>
<hr />
<main>
	<Question />
</main>

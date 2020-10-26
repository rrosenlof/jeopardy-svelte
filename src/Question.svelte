<script>
    import { onMount } from "svelte";
    let question;
    const proxyurl = "https://cors-anywhere.herokuapp.com/";

    onMount(async () => {
        await fetch(
            `${proxyurl}https://jeopardy-rest-api.herokuapp.com/api/v1/jeopardy/questions/random`
        )
            .then((r) => r.json())
            .then((data) => {
                console.dir(data);
                question = data;
            });
    });

    let viewAnswer = false;
    function toggleAnswer() {
        viewAnswer = !viewAnswer;
    }

    function newQuestion() {}
</script>

<style>
    .loading {
        opacity: 0;
        animation: 0.4s 0.8s forwards fade-in;
    }
    @keyframes fade-in {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }
    #q-value {
        font-style: italic;
    }
    .question-comp {
		margin: 0 auto;
		width: 60%;
	}
</style>

<div class="question-comp">
{#if question}
    <div id="question-div">
        <h2>{question.category}</h2>
        <p>Value: <span id="q-value">${question.adj_value2}</span></p>
        <p>{question.question}</p>
        <hr />
        <button on:click={toggleAnswer}>Show/Hide Answer</button>
        {#if viewAnswer}
            <p>{question.answer}</p>
            <!-- <button on:click={newQuestion}>Next Question</button> -->
        {/if}
    </div>
{:else}
    <p class="loading">loading...</p>
{/if}
</div>

<script>
    import { onMount, tick } from "svelte";
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

    async function nextClue(event) {
        viewAnswer = false;
        question = '';
        event.preventDefault();

        fetch(
            `${proxyurl}https://jeopardy-rest-api.herokuapp.com/api/v1/jeopardy/questions/random`
        )
            .then((r) => r.json())
            .then((data) => {
                console.dir(data);
                question = data;
            });

        await tick();
    }
</script>

<style>
    .loading {
        opacity: 0;
        animation: 0.1s 0.8s forwards fade-in;
    }
    @keyframes fade-in {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }

    .question-div {
        padding: 0.3rem 1.3rem;
        background-color: #f3f3f7;
    }

    .question-comp {
        margin: 0 auto;
        width: 90%;
    }
</style>

<div class="question-comp">
    {#if question}
        <div class="question-div">
            <h2><strong>Category: </strong>{question.category}</h2>
            <p><strong>Value: </strong>${question.adj_value2}</p>
            <p>
                <strong>Question: </strong>
                {@html question.question}
            </p>
            <button on:click={toggleAnswer}>Show/Hide Answer</button>
            {#if viewAnswer}
                <p>
                    <strong>Answer: </strong>
                    {@html question.answer}
                </p>
                <button on:click={nextClue}>Next Clue</button>
            {/if}
        </div>
    {:else}
        <p class="loading">loading...</p>
    {/if}
</div>

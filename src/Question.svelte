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

    function viewMoreInfo(question) {
        console.log('viewMoreInfo coming soon',question.id)
    }

    function flagForError(question) {
        console.log('flagForError coming soon',question.id)
    }
</script>

<style type="text/scss">
    $color: #3344ee;
    $color-secondary: #c2c5e8;

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

    .blue-span {
        color: $color;
        font-weight: bold;
    }

    .secondary-button {
        background-color: $color-secondary;
        color: white;
    }

    .warning-button {
        background-color: #f7897f;
        color: white;
    }
</style>

<div class="question-comp">
    {#if question}
        <div class="question-div">
            <h2><span class="blue-span">Category: </span>{question.category}</h2>
            <p><span class="blue-span">Value: </span>${question.adj_value2}</p>
            <p>
                <span class="blue-span">Question: </span>
                {@html question.question}
            </p>
            <button on:click={toggleAnswer}>Show Answer</button>
            {#if viewAnswer}
                <p>
                    <span class="blue-span">Answer: </span>
                    {@html question.answer}
                </p>
                <button on:click={nextClue}>Next Clue</button>
                <button class="secondary-button" on:click={viewMoreInfo(question)}>View More Info</button>
                <button class="warning-button" on:click={flagForError(question)}>Flag for Errors</button>
            {/if}
        </div>
    {:else}
        <p class="loading">Loading...</p>
    {/if}
</div>

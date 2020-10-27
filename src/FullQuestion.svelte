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

</script>

<style type="text/scss">
    $color: #3344ee;

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
</style>

<div>
    <p>Here will be information on a specific question</p>
    <p>{question.question}</p>
</div>

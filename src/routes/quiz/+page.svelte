<script lang="ts">
	const questions = [
		{
			question: 'Is svelte awesome?',
			explanation: 'Yes, svelte is awesome.',
			answer: true
		},
		{
			question: 'Was JavaScript created in 1995?',
			explanation: 'JavaScript was created in 1995.',
			answer: true
		}
	];

	let message: string = 'Please choose between true or false';
	let currentLevel: number = 0;
	let score = {
		correct: 0,
		incorrect: 0
	};
	let gameFinished: boolean = false;

	const submitAnswer = (submittedAnswer: boolean, level: number) => {
		if (submittedAnswer === questions[level].answer) {
			message = 'You got the answer correct.';
			score.correct++;
		} else {
			message = 'You got the answer wrong. Explanation: ' + questions[level].explanation;
			score.incorrect++;
		}

		if (level == questions.length - 1) {
			message = `You finished the quiz! Total correct answers: ${score.correct}, Total incorrect answers: ${score.incorrect}`;
			score.correct = 0;
			score.incorrect = 0;
			gameFinished = true;
		} else {
			currentLevel++;
		}
	};

	const resetQuiz = () => {
		currentLevel = 0;
		message = 'Please choose between true or false';
		gameFinished = false;
	};
</script>

<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<main>
	<h1>JavaScript Quiz with Svelte!</h1>
	{#if !gameFinished}
		<div class="question">{questions[currentLevel].question}</div>
		<div class="buttons">
			<button on:click={() => submitAnswer(true, currentLevel)}>True</button>
			<button on:click={() => submitAnswer(false, currentLevel)}>False</button>
		</div>
	{/if}
	<div class="answer">{message}</div>
	{#if gameFinished}
		<div class="reset">
			<button on:click={() => resetQuiz()}>Reset Quiz</button>
		</div>
	{/if}
</main>

<style>
	.question {
		background-color: rgba(255, 255, 255, 0.2);
		border-radius: 20px;
		padding: 20px;
		width: 100%;
		text-align: center;
		font-size: 36px;
	}

	.buttons {
		margin: 20px;
		display: flex;
		gap: 10px;
		align-items: center;
		justify-content: center;
	}

	button {
		background-color: rgba(255, 255, 255, 0.3);
		border-radius: 20px;
		border: none;
		color: white;
		cursor: pointer;
		padding: 10px 30px;
	}

	button:active {
		background-color: rgba(255, 255, 255, 0.1);
	}

	button:hover {
		background-color: rgba(255, 255, 255, 0.2);
	}

	.answer {
		width: 100%;
		display: flex;
		justify-content: center;
	}

	.reset {
		margin-top: 40px;
		width: 100%;
		display: flex;
		justify-content: center;
	}
</style>

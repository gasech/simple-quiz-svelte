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

	let gameState = {
		score: {
			correct: 0,
			incorrect: 0
		},
		gameFinished: false,
		message: 'Please choose between true or false',
		currentLevel: 0
	};

	const submitAnswer = (submittedAnswer: boolean) => {
		if (submittedAnswer === questions[gameState.currentLevel].answer) {
			gameState.message = 'You got the answer correct.';
			gameState.score.correct++;
		} else {
			gameState.message =
				'You got the answer wrong. Explanation: ' + questions[gameState.currentLevel].explanation;
			gameState.score.incorrect++;
		}

		if (gameState.currentLevel == questions.length - 1) {
			gameState.message = `You finished the quiz! 
                    Total correct answers: ${gameState.score.correct}, 
                    Total incorrect answers: ${gameState.score.incorrect}`;
			gameState.score.correct = 0;
			gameState.score.incorrect = 0;
			gameState.gameFinished = true;
		} else {
			gameState.currentLevel++;
		}
	};

	const resetQuiz = () => {
		gameState.currentLevel = 0;
		gameState.message = 'Please choose between true or false';
		gameState.gameFinished = false;
	};
</script>

<svelte:head>
	<title>Svelte Quiz</title>
	<meta name="description" content="Quiz" />
</svelte:head>

<main>
	<h1>JavaScript Quiz with Svelte!</h1>
	{#if !gameState.gameFinished}
		<div class="question">{questions[gameState.currentLevel].question}</div>
		<div class="buttons">
			<button on:click={() => submitAnswer(true)}>True</button>
			<button on:click={() => submitAnswer(false)}>False</button>
		</div>
	{/if}
	<div class="answer">{gameState.message}</div>
	{#if gameState.gameFinished}
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

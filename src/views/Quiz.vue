<template>
  	<main class="quiz">
		<section class="quiz__questions">
			<div class="questions__question">
				Quiz

				<div class="question__query">
					{{ currentQuestion.query }}
				</div>
			</div>

			<div class="questions__options">
				<button class="options__option" v-for="option in currentQuestion.options" @click="optionClicked(option)">
					{{ option }}
				</button>
				
				<div class="options__buttons">
					<button @click="nextQuestion" v-if="index < 3">
						<svg width="50" height="50" viewBox="0 0 50 50" fill="none" xmlns="http://www.w3.org/2000/svg">
							<path d="M40.9997 25.094L9.00024 24.9059" stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
							<path d="M26.9176 39.0115L40.9997 25.094L27.0822 11.012" stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
						</svg>
					</button>

					<button class="options__start-over" @click="startOver" v-else>
						<svg width="80" height="80" viewBox="0 0 69 69" fill="none" xmlns="http://www.w3.org/2000/svg">
							<path d="M34.5 0C15.4462 0 0 15.4462 0 34.5C0 53.5538 15.4462 69 34.5 69C47.2886 69 58.4424 62.0365 64.4012 51.6995L52.2554 44.7127C48.715 50.8533 42.0973 54.997 34.5 54.997C23.1798 54.997 14.003 45.8202 14.003 34.5C14.003 23.1798 23.1798 14.003 34.5 14.003C39.3523 14.003 43.7996 15.7004 47.3069 18.5218L38.2482 24.9654L69 35.2201V3.08275L58.9852 10.2085C52.7346 3.90724 44.0768 0 34.5 0Z" fill="black"/>
						</svg>
					</button>
				</div>
			</div>
		</section>

		<section class="quiz__score">
			<div class="score__title">Score</div>
			
			<div class="score__points">
				Your score is {{ score }}/3
			</div>
		</section>
    </main>
</template>

<script>
	export default {
		data() {
			return {
				index: 0,
				score: 0,
				lastOption: null,
				questions: [
					{
						query: "What is the capital of Madagaskar?",
						options: { a: "Mugadishu", b: "Marrakesh", c: "Dodoma", d: "Antananarivo" },
						correctAnswer: "d",
					},
					{
						query: "What is the capital of Norway?",
						options: { a: "Oslo", b: "Skien", c: "Tomter", d: "Tøyen" },
						correctAnswer: "a",
					},
					{
						query: "What is the capital of Greenland?",
						options: { a: "Stockholm", b: "Berlin", c: "Nuuk", d: "Virenze" },
						correctAnswer: "c",
					},
					{
						query: "Do you want to start over?"
					}
				],
			};
		},

		computed: {
			currentQuestion() {
				return this.questions[this.index];
			},

			correctAnswer() {
				return this.currentQuestion.options[this.currentQuestion.correctAnswer]
			}
		},

		methods: {
			optionClicked(option) {
				this.lastOption = option;
			},

			nextQuestion() {
				this.updateScore();
				this.increaseIndex();
			},

			increaseIndex() {
				this.index = this.index === this.questions.length - 1 ? 0 : this.index + 1;
			},

			updateScore() {	
				if (this.score < 3 && this.lastOption === this.correctAnswer) {
					this.score += 1;
				} else {
					this.score += 0;
				}
			},
			
			startOver() {
				this.score = 0;
				this.index = 0;
			}
		}
	};
</script>

<!--
	1 Lager to computed funksjoner
		1.1 CurrentQuestion, returnerer riktig index
		1.2 CorrectAnswer, returner riktig svar utifra options
	2 Lager fem methods funksjoner
		2.1 OptionClicked, henter option som du trykker på og sier at this.lastOption er option
		2.2 NextQuestion, kjører to funksjoner
		2.3 IncreaseIndex, hvis this.index er samme som questions.length - 1, så this.index + 1,
			og da har vi skrevet at hvis index blir over 3 får man opp en start-over-knapp
		2.4 UpdateScore, hvis this.score er mindre enn 3 OG lastOption er samme som correctAnswer,
			så blir scoren + 1, hvis ikke + 0
		2.5 StartOver, setter index = 0 og score = 0
-->

<style>
	.quiz {
 		display: flex;
  		margin-top: 20px;
		width: 100vw;
	}

	.quiz__questions {
  		width: 60%;
  		padding: 20px;
  		display: flex;
		padding-left: 100px;
	}

	.questions__question {
		width: 30vw;
		font-size: 3em;
		font-weight: bold;
	}

	.question__query {
		margin-top: 20px;
		font-size: 0.6em;
		font-weight: 100;
	}

	.questions__options {
		display: grid;
		height: 50vh;
		margin: 200px 0px 0px 0px;
		grid-gap: 30px;
		width: 15vw;
	}

	.options__option {
		background-color: beige;
		border: 1px solid beige;
	}

	.options__option:hover {
		border: black 1px solid;
	}

	.options__option:focus {
		background-color: black;
		color: white;
	}

	.options__buttons {
		display: flex;
		justify-content: right;
	}

	.options__start-over {
		height: fit-content;
		margin-top: 150px;
	}

	.options__start-over:hover {
		transform: rotate(360deg);
		transition-duration: 1.3s;
	}

	.quiz__score {
		width: 40%;
		border-left: 2px solid black;
		height: 85vh;
		padding: 20px;
		padding-left: 40px;
	}

	.score__title {
		font-size: 3em;
		font-weight: bold;
	}

	.score__points {
		font-size: 1.3em;
		margin-top: 20px;
		margin-bottom: 20px;
	}
</style>
<template>
	<div>
		<div v-if="isQuizStarted">
			<h4>{{ operandLeft }} {{ operator }} {{ operandRight }}</h4>

			<button
				@click="selectedAnswer(answer)"
				v-for="(answer, index) of answers"
				:key="index"
			>
				{{ answer }}
			</button>
		</div>

		<div v-if="!isQuizStarted">
			<button @click="startQuiz">start</button>
		</div>

		<button @click="$emit('onBack')">Back</button>
	</div>
</template>

<script>
export default {
	name: 'OperatorQuiz',
	props: ['operator'],
	data() {
		return {
			isQuizStarted: false,
			operandLeft: null,
			operandRight: null,
			answers: [],
			expectedAnswer: null,
		};
	},
	methods: {
		selectedAnswer(answerSelected) {
			if (answerSelected !== this.expectedAnswer) {
				alert('WRONG ANSWER!');
			}
			this.startQuiz();
		},
		startQuiz() {
			this.isQuizStarted = true;

			do {
				this.operandLeft = parseInt(Math.random() * 13);
				this.operandRight = parseInt(Math.random() * 13);
			} while (
				this.operator === '/' &&
				(this.operandLeft === 0 || this.operandRight === 0)
			);

			const methods = {
					'+': (a, b) => a + b,
					'-': (a, b) => a - b,
					'/': (a, b) => a / b,
					'*': (a, b) => a * b,
				},
				methodToUse = methods[this.operator];

			this.answers = [];

			while (this.answers.length < 5) {
				let answer = methodToUse(
					Math.floor(Math.random() * 13),
					Math.floor(Math.random() * 13)
				);

				let isTheAnswer =
					methodToUse(this.operandLeft, this.operandRight) === answer;

				if (answer % 1 !== 0) {
					answer = parseFloat(answer.toFixed(3));
				}

				let isRepeated = this.answers.findIndex((n) => n === answer);

				if (
					!isNaN(answer) &&
					answer !== Infinity &&
					isRepeated < 0 &&
					!isTheAnswer
				) {
					this.answers.push(answer);
				}
			}

			let expectedAnswer = methodToUse(this.operandLeft, this.operandRight);

			if (expectedAnswer % 1 !== 0) {
				expectedAnswer = parseFloat(expectedAnswer.toFixed(3));
			}

			this.answers[
				parseInt(Math.random() * this.answers.length)
			] = expectedAnswer;

			this.expectedAnswer = expectedAnswer;
		},
	},
};
</script>

<style></style>

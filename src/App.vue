<template>
	<div id="app">
		<h1>Math Quiz App</h1>
		<OperatorQuiz
			v-if="operator"
			@onBack="clearOperator"
			:operator="operator"
		/>
		<OperatorSelector v-if="!operator" @changeOperator="selectOperator" />
	</div>
</template>

<script>
import OperatorSelector from './components/OperatorSelector.vue';
import OperatorQuiz from './components/OperatorQuiz.vue';

export default {
	name: 'App',
	data() {
		return {
			operator: null,
		};
	},
	methods: {
		selectOperator(operator) {
			this.operator = operator;
		},
		clearOperator() {
			this.operator = null;
		},
	},
	components: {
		OperatorSelector,
		OperatorQuiz,
	},
};
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
	font-size: 24px;
}

button {
	padding: 10px;
	min-width: 160px;
	height: 80px;
	margin: 6px;
	background-color: #10aeb2;
	color: white;
	font-size: 24px;
	cursor: pointer;
	vertical-align: top;
	border: none;
}
</style>

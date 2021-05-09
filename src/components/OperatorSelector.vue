<template>
	<div>
		<button @click="$emit('changeOperator', '+')">
			Adition <br />
			+
		</button>
		<button @click="$emit('changeOperator', '-')">
			Substraction <br />
			-
		</button>
		<button @click="$emit('changeOperator', '/')">
			Division <br />
			/
		</button>
		<button @click="$emit('changeOperator', '*')">
			Multiplication <br />
			*
		</button>
	</div>
</template>

<script>
export default {
	name: 'OperatorSelector',
};
</script>

<style></style>

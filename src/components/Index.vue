<template>
	<div class="p-3" style="max-width: 400px; margin: 50px auto; background-color: #234">
		<!-- Calculator Result -->
		<h1 style="color: white; text-align: center">Merry Chrismas</h1>
		<div class="w-full rounded m-1 p-3 text-right font-weight-bold text-white bg-vue-dark">
			{{ calculatorValue || 0 }}
		</div>

		<!-- Calculator Buttons  -->
		<div class="row no-gutters">
			<div class="col-3" v-for="n in calculatorElements" :key="n">
				<div
					class="lead text-white text-center m-2 py-3 bg-vue-dark rounded hover-class"
					:class="{ 'bg-vue-green': ['C', '*', '/', '-', '+', '%', '='].includes(n) }"
					@click="action(n)"
				>
					{{ n }}
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "Index",
	props: {
		msg: String,
	},
	data() {
		return {
			calculatorValue: "",
			calculatorElements: [
				"C",
				"*",
				"/",
				"-",
				7,
				8,
				9,
				"+",
				4,
				5,
				6,
				"%",
				1,
				2,
				3,
				"=",
				0,
				".",
			],
			operator: null,
			previousCalculatorValue: "",
		};
	},
	methods: {
		action(n) {
			// Append Value
			if (!isNaN(n) || n === ".") {
				this.calculatorValue += n + "";
			}

			// Clear Value
			if (n === "C") {
				this.calculatorValue = "";
			}

			// Percentage
			if (n === "%") {
				this.calculatorValue = this.calculatorValue / 100 + "";
			}

			// Operators
			if (["/", "*", "-", "+"].includes(n)) {
				this.operator = n;
				this.previousCalculatorValue = this.calculatorValue;
				this.calculatorValue = "";
			}

			if (n === "=") {
				this.calculatorValue = eval(
					this.previousCalculatorValue + this.operator + this.calculatorValue
				);

				this.previousCalculatorValue = "";
				this.operator = "null";
			}
		},
	},
};
</script>

<style scoped>
.bg-vue-dark {
	background: #31475e;
}

.hover-class {
	transition: 0.5s ease;
}

.hover-class:hover {
	cursor: pointer;
	background: #3d5875;
}

.bg-vue-green {
	background: #3fb984;
}
</style>

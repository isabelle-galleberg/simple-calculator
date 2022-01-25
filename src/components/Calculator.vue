<template>
	<div class="calculator">
		<div class="display">{{ current || "0" }}</div>
		<div @click="clear" class="btn operator2">AC</div>
		<div @click="sign" class="btn operator2">+/-</div>
		<div @click="percent" class="btn operator2">%</div>
		<div @click="divide" class="btn operator">÷</div>
		<div @click="append('7')" class="btn">7</div>
		<div @click="append('8')" class="btn">8</div>
		<div @click="append('9')" class="btn">9</div>
		<div @click="times" class="btn operator">x</div>
		<div @click="append('4')" class="btn">4</div>
		<div @click="append('5')" class="btn">5</div>
		<div @click="append('6')" class="btn">6</div>
		<div @click="minus" class="btn operator">-</div>
		<div @click="append('1')" class="btn">1</div>
		<div @click="append('2')" class="btn">2</div>
		<div @click="append('3')" class="btn">3</div>
		<div @click="add" class="btn operator">+</div>
		<div @click="append(0)" class="btn zero">0</div>
		<div @click="dot" class="btn">.</div>
		<div @click="equal" class="btn operator">=</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			previous: null,
			current: "",
			operator: null,
			operatorClicked: false,
		};
	},
	methods: {
		clear() {
			this.current = "";
		},
		sign() {
			this.current =
				this.current.charAt(0) === "-"
					? this.current.slice(1)
					: `-${this.current}`;
		},
		percent() {
			this.current = `${parseFloat(this.current) / 100}`;
		},
		append(number) {
			if (this.operatorClicked) {
				this.current = this.current = "";
				this.operatorClicked = false;
			}
			this.current = `${this.current}${number}`; //concatenates strings
		},
		dot() {
			if (this.current.indexOf(".") === -1) {
				this.append(".");
			}
		},
		setPrevious() {
			this.previous = this.current;
			this.operatorClicked = true;
		},
		divide() {
			this.operator = (a, b) => a / b;
			this.setPrevious();
		},
		times() {
			this.operator = (a, b) => a * b;
			this.setPrevious();
		},
		minus() {
			this.operator = (a, b) => a - b;
			this.setPrevious();
		},
		add() {
			this.operator = (a, b) => a + b;
			this.setPrevious();
		},
		equal() {
			this.current = `${this.operator(
				parseFloat(this.current),
				parseFloat(this.previous)
			)}`;
			this.previous = null;
		},
	},
};
</script>

<style>
body {
	background-color: #333;
}

.calculator {
	width: 350px;
	font-size: 40px;
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	grid-auto-rows: minmax(50px, auto);
	margin-left: 50px;
}

.display {
	grid-column: 1/5;
	color: white;
}

.btn {
	background-color: #505050;
	color: white;
	border-radius: 50%;
	margin: 10px;
	padding: 5px;
	box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.btn:hover {
	opacity: 0.5;
}

.zero {
	grid-column: 1/3;
}

.operator {
	background-color: orange;
}

.operator2 {
	background-color: #cccccc;
	color: black;
}
</style>

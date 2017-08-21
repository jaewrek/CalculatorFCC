<template>
	<div class="calculator">
		<h1>VueJS Calculator</h1>
		<div @click="register" class="flex">
			<div class="screen take4">
			{{ display }}
				<div class="process">{{ processing }}</div>	
			</div>
			<div class="ac take1">AC</div>
			<div class="ce take1">CE</div>
			<div class="modulo take1">%</div>
			<div class="divide take1">/</div>
			<div class="seven take1">7</div>
			<div class="eight take1">8</div>
			<div class="nine take1">9</div>
			<div class="multiply take1">*</div>
			<div class="four take1">4</div>
			<div class="five take1">5</div>
			<div class="six take1">6</div>
			<div class="minus take1">-</div>
			<div class="one take1">1</div>
			<div class="two take1">2</div>
			<div class="three take1">3</div>
			<div class="plus take1">+</div>
			<div class="zero take2">0</div>
			<div class="period take1">.</div>
			<div class="equal take1">=</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'calculator',
	data() {
		return {
			reset: false,
			display: 0,
			calculate: '',
			operations: []

		}
	},
	mounted(){
		
	},
	computed: {
		processing() {
			if(this.operations.length < 1){
				return 0
			} else {
			return this.operations.join('');
		}
		},
		displayLimit() {
			}		
		
	},
	methods: {
		register() {
			let input = event.target.innerHTML;

			if(input.length > 2){
				return
			}
			if (this.display == 0 || /[^0-9\.]/.test(this.display)){
					this.display = input;
					
			} else if (/[0-9]/.test(input) ) {
				if(this.reset){
					console.log("ME")
					this.operations = [];
					this.display = input;
					this.reset = false;
				} else {this.display = this.display.toString() + input.toString();}
			}

			if (/[^0-9]/.test(input)) {
				if(this.reset){
					this.operations = [];
					// this.operations.push(this.display)
					this.reset = false;
				}
				switch(input) {
					case '/':
						this.operation('/')
						break;
					case '*':
						this.operation('*')
						break;
					case '+':
						this.operation('+')
						break;
					case '-':
						this.operation('-')
						break;
					case '%':
						this.operation('%')
						break;
					case '.':
						this.period(input)
						break;
					case '=':
						this.equals()
						break;
					case 'AC':
						this.ac()
						break;
					case 'CE':
						this.ce()
						break;
				}
			}
			
		},
		operation(op){
			// console.log(this.operations);
			if(/\d+/.test(this.display)){
				this.operations.push(Number(this.display));
			}
			
			this.pushOperation(op);
			this.display = op;
		},
		pushOperation(op) {
			if(/\d+/.test(this.operations[this.operations.length-1])){
				this.operations.push(op);
			}
		},
		subtraction() {
			this.operations.push('-')
			this.a = this.display;
			this.display = '-';
		},
		ce() {
			this.display = 0
		},
		ac() {
			this.display = 0
			this.operations = []
		},
		period(input) {
			console.log("period")
			this.display = this.display.toString() + input.toString();
		},
		equals(){
			this.operations.push(this.display);
			this.calculate = this.operations.join('');
			this.display = eval(this.calculate)
			console.log(this.display.toString().length)
			if(this.display > 10000000 &&
				this.display.toString().length > 8){
				this.display = this.display.toExponential(3);

			} else
			if(this.display.toString().length > 8){
				this.display = this.display.toFixed(3);
			} 
			
			this.reset = true;
			
		}
	}
	
}
</script>

<stylus>
.calculator
	color: teal
.flex
	background-color: black
	border: 1px solid black
	border-radius: 30px
	padding: 2% 1% 3% 1%
	display: flex
	justify-content: center
	align-content: center
	align-items: center
	flex-wrap: wrap
	margin: 1% 40%
	font-size: 1.5em
	font-weight: bold
	.take4
		flex: 1 0 100%
		
	.take1
		flex: 1 0 25%
		
	.take2
		flex: 1 0 50%
.screen
	height: 10%
	border: 1px solid black
	border-radius: 10px
	background-color: #f3f3f3	
	margin-bottom: 2%
	text-align: right
	font-size: 2em
	padding-right: 1%
	.process
		font-size: .2em
.take15, .take1, .take2
	border: 2px solid black
	border-radius: 10px
	background-color: #d3d3d3
	box-sizing: border-box
	height: 10%
.ac, .ce 
	background-color: #ff6961

</stylus>
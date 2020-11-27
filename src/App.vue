<template>
	<div id="app">
		<img class="img" src="./assets/cronometro.png" alt="Imagem do cronometro">
		<a class="timer">
			{{this.number}}
		</a>
		<div class="btn-area">
			<div class="primary-button">
				<button class="btn" @click="go()">{{this.button}}</button>
				<button class="btn" @click="zerar()">Zerar</button>
			</div>
			<div class="btn-clear-history" v-show="this.history.length > 0">
				<button class="btn" @click="clear()">limpar historico</button>
			</div>
		</div>

		<div v-show="this.history.length > 0" class="history-area">
			<h4>Historico de pausas</h4>
			<div class="history-single" v-for="(historySingle, index) in this.history" :key="index">
				Você pausou em: {{historySingle}}
			</div>
		</div>
	</div>
</template>

<script>

export default {
	name: 'App',
	data() {
		return {
			number: '00:00:00',
			button: 'VAI',
			timer: null,
			ss: 0,
			mm: 0,
			hh: 0,
			history: []
		}
	},
	components: {
		
	},
	methods: {
		
		go: function() {
			if(this.timer == null) {
				this.timer = setInterval(()=>{
					this.runCountdown();
				}, 1000);
				this.button = 'PAUSAR';
			} else {
				clearInterval(this.timer);
				this.timer = null;
				this.button = 'CONTINUAR';
				this.history.push(this.number)
			}
		},
		
		zerar: function() {
			clearInterval(this.timer);
			this.timer = null;
			this.button = 'VAI';
			this.number = '00:00:00';
			this.ss = 0;
			this.mm = 0;
			this.hh = 0;
			this.clearHistory();
		},
		
		clear: function() {
			this.clearHistory();
		},

		runCountdown: function() {
			
			this.ss++;
			if(this.ss > 59) {
				this.mm++;
				this.ss = 0;
			}

			if(this.mm > 59) {
				this.hh++;
				this.mm = 0;
			}

			var format = (this.hh < 10 ? '0' + this.hh : this.hh) + ':' 
			+ (this.mm < 10 ? '0' + this.mm : this.mm)+ ':' 
			+ (this.ss < 10 ? '0' + this.ss : this.ss);
			return this.number = format;
		},
		clearHistory: function() {
			var contador = this.history.length;
			var i = 0;

			while(i < contador) {
				this.history.pop();
				i++;
			}
		}
	}
}
</script>

<style>

	#app {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
	}

	.img {
		width: 350px;
		height: 350px;
		padding-top: 100px;
	}

	.timer {
		color: #fff;
		font-size: 30px;
		margin-top: -170px;
	}

	.btn-area {
		margin-top: 170px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.btn-clear-history {
		margin-top: 10px;
	}

	.btn {
		-webkit-user-select: none;
		-moz-user-select: none;
		padding: 6px;
		font-size: 16px;
		width: 130px;
		margin: 0 10px;
		cursor: pointer;
		border: 0;
		outline: 0;
		transition: all 0.8s;
	}

	.btn:hover {
		opacity: 0.8;
		transition: all 0.8s;
	}

	.history-area {
		width: 300px;
		background-color: #2d3129;
		margin: 10px 0;
		color: #ccc;
		padding: 5px;
		border-radius: 10px;
		border: 1px solid #2d302b;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.history-single {
		margin-bottom: 4px;
	}
</style>

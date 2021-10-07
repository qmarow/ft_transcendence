<template>
	<div class="container">
		<span class="trunc">ft_transcendence</span>
		<div class="blockInput">
			<input type="text" class="input login" placeholder="Login" v-model="username"/>
			<input type="password" class="input pass" placeholder="password" v-model="password"/>
			<button class="reg" @click="registration">registration</button>
			<span v-if="errorLog" class="errorLog error">Login must contain more than 4 characters and less than 8</span>
			<span v-if="errorPass" class="errorPass error">Password must contain more than 4 characters and less than 8</span>
		</div>
		<router-link to="/auth" class="ref">
			<img class="photo" src="./../images/autor.svg" />
			<div class="textReg">
				autorisation
			</div>
		</router-link>
	</div>
</template>


<script>
import axios from 'axios'
export default {
	props: {},
	emits: ['sing', 'getDataUser'],
	data() {
		return {
			username: '',
			password: '',
			errorLog: false,
			errorPass: false,
		}
},
	methods: {
		registration(){
			if (!this.errorPass && !this.errorLog) {
				axios('/api/user/registration', {
					method: 'POST',
					data: {
						user: {
							username: this.username,
							password: this.password
						}
					}
				}).then(response => {
					alert("Вы успешно зарегестрировались! Запомните его, потому что если ты долбаеб забудешь его, мы не предусмотрели возможность сбросить пароль. Твоя учетная запись будет потеряна")
					this.$emit("getDataUser", response.data.user);
					this.$emit('sing');
				}).catch(() => {
					alert("Вы ввели неверный пароль или логин. Или такой пользователь уже есть ")
				})
			}
		}
	},
	watch: {
		username: function(newLogin) {
			console.log("!!!!!!!!");
			this.errorLog = false;
			if (newLogin.length > 8 || newLogin.length < 4) {
				this.errorLog = true;
			}
		},
		password: function(newPass) {
			this.errorPass = false;
			if (newPass.length > 8 || newPass.length < 4) {
				this.errorPass = true;
			}
		}
	},
	components: {}
}
</script>


<style scoped>

.error {
	color: rgb(255, 72, 72);
	font-size: 20px;
	display: inline-block;
	width: 280px;
	position: absolute;
	word-break: break-all;
}

.errorLog {
	left: 220px;
	top: 6px;
}

.errorPass {
	left: 220px;
	top: 73px;
}

.textReg {
	font-size: 30px;
	color:rgb(151, 150, 150);
	text-decoration: none;
}

.container {
	display: flex;
	height: 100vh;
	flex-direction: column;
	justify-content: space-between;
	align-items: center;
}
.blockInput {
	display: flex;
	flex-direction: column;
	align-items: center;
	position: relative;
}

.reg:hover {
	background-color: rgb(123, 187, 107);
}

.reg {
	width: 197px;
	height: 53.03px;
	font-size: 30px;
	border-radius: 17px;
	margin-top: 15px;
	border: 1.5px #4F4F4F solid;
	
	background-color: #767373;
	font-family: UnicaOne;
	font-style: normal;
	font-weight: normal;
	align-items: center;
	text-align: center;
	letter-spacing: -0.03em;
}

.photo {
	width: 62px;
	height: 62px;
}

.pass {
	margin-top: 10px;
	width: 197px;
	height: 53.03px;
	font-size: 30px;
	border-radius: 17px;
}

.login {
	width: 197px;
	height: 53.03px;
	font-size: 30px;
	border-radius: 17px;
}

.trunc {
	margin-top: 90px;
	font-style: normal;
	font-weight: normal;
	font-size: 140px;
	letter-spacing: -0.03em;

	color: #7663EF;
}

.ref {
	text-decoration: none;
	display: flex;
	align-items: center;
	flex-direction: column;
}

</style>
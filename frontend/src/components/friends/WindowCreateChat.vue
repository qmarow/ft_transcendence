<template>
	<div id="window">
		<div id="blockPhoto">
			<img id="img" src="./../../images/image.svg"/>
			<div id="upload">
				<img :style="{'width':'11px'}" src="./../../images/iconDownloud.svg">
				<span>upload photo</span>
			</div>
		</div>
		<input v-model="data.name" class="inputTxt" type="text" placeholder="name chat"/>
		<div id="blockCheckBox">
			<input v-model="isClosed" id="inputCheckBox" type="checkbox">
			<span>Closed</span>
		</div>
		<input v-model="data.pass" class="inputTxt pass" type="password" placeholder="password"/>
		<div v-if="!isClosed" id="closePass"></div>
		<button @click="$emit('getData', data)" id="btn">create</button>
	</div>
</template>


<script>
export default {
	props: {},
	emits: ['getData'],
	data() {
		return {
			isClosed: false,
			data: {
				name: '',
				pass: '',
			}
		};
},
	components: {}
}
</script>


<style scoped>

#window {
	padding: 25px;
	display: flex;
	flex-direction: column;
	align-items: center;
	position: relative;
	width: 349px;
	height: fit-content;
	background: rgba(49, 49, 50, 1);
	border: 1px solid rgba(64, 67, 69, 1);
	border-radius: 21px;
	box-shadow: 1px 3px 4px 0px #000;
}

#blockPhoto {
	position: relative;
	padding-bottom: 10px;
}

#upload {
	width: 90px;
	position: absolute;
	top: 120px;
	left: 0px;
} #upload span {
	font-size: 13px;
	margin-left: 4px;
	color: #968686;
}
#img {
	width: 135px;
	height: auto;
}

.inputTxt {
	font-family: UnicaOne;
	text-align: center;
	margin-top: 15px;
	width: 197px;
	height: 57px;
	font-size: 30px;
	color: rgba(255, 255, 255, 0.38);
	border: 1px solid #968686;
	box-sizing: border-box;
	border-radius: 17px;
	background-color: rgba(230, 230, 250, 0);
}
.pass {
	margin-top: 10px;
}

#blockCheckBox {
	display: flex;
	align-items:flex-end;
	width: 197px;
	margin-top: 10px
} #blockCheckBox span {
	font-size: 20px;
	margin-left: 8px;
	color: rgba(255, 255, 255, 0.38);
}

#inputCheckBox {
	width: 30px;
	height: 30px;
}

#closePass {
	position: absolute;
	top: 291px;
	background-color: rgba(87, 87, 87, 0.712);
	width: 197px;
	height: 57px;
	border-radius: 17px;
}

#btn {
	margin-top: 15px;
	width: 108px;
	height: 44px;
	border-radius: 26px;
	border: 0px;
	font-family: UnicaOne;
	font-style: normal;
	font-weight: normal;
	font-size: 22px;
	background-color: #2FA0DF;
	transition: .2s;
} #btn:hover {
	transform: translateY(-2px);
	background-color: #28b4ff;
}

</style>
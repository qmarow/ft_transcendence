<template>
	<div id="blockChat">
		<div id="visibleChat" v-if="dataChat != null">
			<span id="title">{{dataChat.name}}</span>
			<hr>
			<div id="chat">
				<div class='mess'>
					<img v-if="true" class="imgMess" src="./../../images/image.svg">
					<span class="txtMess" :class="(true) ? 'otherMess' : 'myMess'">dadfafafadfadfa,df;,ald;f,;as</span>
				</div>
				<div class='mess'>
					<img v-if="false" class="imgMess" src="./../../images/image.svg">
					<span class="txtMess" :class="(false) ? 'otherMess' : 'myMess'">dalf,;aadfafafadfadfa,df;,ald;f,;as</span>
				</div>
				<div class='mess'>
					<img v-if="true" class="imgMess" src="./../../images/image.svg">
					<span class="txtMess" :class="(true) ? 'otherMess' : 'myMess'">dadfafafalf,af;l,da;f,;ad,f;,as;df;asdf;la;sd,fl;,asdf;;aldf,;ad,f;a,ds;f,a;sd,f;a,;ad,fl;a,df;aldf,;a,df;alfa,df;,ald;f,;as</span>
				</div>
				<div class='mess'>
					<img v-if="false" class="imgMess" src="./../../images/image.svg">
					<span class="txtMess" :class="(false) ? 'otherMess' : 'myMess'">dalf,;aadfafafadfad;d,f; djio;lnkloida;knk;clfjafj lakdjflkajdfkladjf;j;dajf;jadfkafjfjkdajfkdjkafjkladfjklakjldfjklafdkjl;ad;fjkladfjklf;,ald;f,;as</span>
				</div>
			</div>		
			<hr>
			<div class="blockInputMess">
				<img class="imgFight" src="./../../images/iconFight.svg">
				<input type="text" class="inputMess" placeholder="Messege"/>
			</div>
		</div>
		<div id="unVisibleChat" v-if="dataChat == null"> Select Chat</div>
	</div>
</template>


<script>
export default {
	props: ['dataChat'],
	data() {
		return {}
},
	components: {}
}
</script>


<style scoped>

#blockChat {
	background: rgba(49, 49, 50, 1);
	width: 100%;
	height: 653px;
	background: #313132;
	border: 1px solid #404345;
	box-sizing: border-box;
	border-radius: 21px;
}

#visibleChat {
	height: 100%;
	border-radius: 21px;
}

#unVisibleChat {
	display: flex;
	justify-content: center;
	align-items: center;
	color:rgb(109, 100, 99);
	background-color: rgba(63, 63, 63, 0.438);
	height: 100%;
	border-radius: 21px;
	font-size: 50px;

}

#chat {
	/* background-color: lemonchiffon; */
	height: calc(100% - 120px);
	overflow: auto;
	flex-direction: column;
	box-sizing: border-box;
}

.mess {
	display: flex;
	align-items:flex-end;
	min-height: 40px;
	border-radius: 21px;
	margin-top: 16px;
	font-size: 30px;
	box-sizing: border-box;
	padding: 4px 12px;
	word-break: break-all;
}

.imgMess {
	height: 47px;
	margin-right: 8px;
}

.txtMess {
	display: inline-block;
	height: 100%;
	width: 530px;
	border: 1px solid #4C555F;
	box-sizing: border-box;
	border-radius: 21px;
	padding: 5px 10px;
}

.myMess {
	background: rgba(144, 160, 217, 1);
	margin-left: 55%;
}

.otherMess {
	background: #514B4B;
	max-width: calc(45% - 5%)
}

#title {
	display: block;
	font-size: 48px;
	color: #8D8D8D;
	text-align: center;
	padding: 3px;
}

.blockInputMess {
	display: flex;
	align-items: center;
	height: 55px;
} .blockInputMess:focus {
	border: 1px solid rgb(87, 0, 0)
}

.imgFight {
	height: 50px;
	width: 55px;
	margin-left: 24px;
}

.inputMess {
	text-align: end;
	font-family: UnicaOne;
	margin-left: 40px;
	width: 86%;
	height: 50%;
	font-size: 28px;
	line-height: 33px;
	color: rgba(255, 255, 255, 0.38);
	background-color: rgba(176, 196, 222, 0);
	border: 0px;
	outline: none;
}

hr {
	height: 1px;
	border: 0px;
	background-color: #404345;
	margin: 0px;
}

</style>
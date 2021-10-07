<template>
  <div id="main">
    <div id="choseOfDialogueType">
      <span class="txtType"
      :class="typeActive == 'chats' ? 'active' : ''"
      @click="$emit('getActive', 'chats')">Chats</span>
      <span class="txtType"
      :class="typeActive == 'friends' ? 'active' : ''"
      @click="$emit('getActive', 'friends')">friends</span>
			<span @click="typeActive == 'friends' ? goToModule('/world') : $emit('createChat')"
				class="txtType">{{typeActive == 'chats' ? 'Add chat': 'Add user'}}</span>
		</div>
		<hr>
		<div id="scrollBar">
			<div @click="$emit('selectedChat', elem)" class="elemOfScrollBar" v-for="(elem, i) of data" :key="i">
				<div class="blockImg">  
					<img class="img" :style="getColor(elem.status)" :src="require('./../../' + elem.images)"/>
					<div v-if="elem.type == 'friendInvitation'" id="blockToReplyInvitation">
						<div class="btn" style="">
							<span class="plus"></span>
						</div>
						<div class="btn" style="background-color: rgb(206, 61, 61)">
							<span class="minus"></span>
						</div>
					</div>
					<span v-if="elem.numberOfMissed > 0" id="numOfMissed">{{elem.numberOfMissed}}</span>
				</div>
				<span class="name">{{elem.name}}</span>
			</div>
		</div>
		<hr>
  </div>
</template>


<script>

export default {
  props: ['typeActive', 'data'],
  emits: ['getActive', 'createChat', 'selectedChat'],
  inject: ['getTocken'],
  mounted() {
    // axios({
    //   method: get,
    //   url: '',
    //   headers: {
    //     'Authorization': `Basic ${this.getTocken()}`
    //   }
    // })
  },
  data() {
    return {
      
    }
  },
  methods: {
    getColor(status) {

      if (status == 'online') {
        return ('border: 2px solid rgba(55, 195, 94, 1)')
      } else if (status == 'offline') {
        return ('border: 2px solid rgba(219, 65, 65, 1)')
      } else {
        return ('border: 2px solid #E2CF8D')
      }
    },
		goToModule(path) {
			this.$router.push(path);
		}
  },
  components: {
	}
}
</script>


<style scoped>

#main {
  display: flex;
	width: 1200px;
	/* background-color: rgb(252, 138, 138); */
}
.txtType {
  width: 100px;
	box-sizing: border-box;
  text-align: center;
  padding: 2.5px 10px;
  border-radius: 13px;
  font-size: 20px;
  transition: .2s;
  background-color: rgba(49, 49, 50, 1);
	margin-top: 4px;
}.txtType:last-child {
	background-color: rgb(143, 252, 133);
  margin-top: 8px;
} .txtType:hover {
  background-color: #2FA0DF;
} .txtType:last-child:hover {
	background-color: rgb(88, 248, 73);
}

.active {
  background-color: #2FA0DF;
}

#choseOfDialogueType {
  display: flex;
  flex-direction: column;
	justify-content: center;
	min-width: 110px;
}

hr {
	width: 2px;
	border: 0px;
	background-color: rgb(58, 58, 58);
}

#scrollBar {
	display: flex;
	overflow: auto;
	/* background-color: lavenderblush; */
	/* border: 2px solid rgb(114, 104, 104);
	border-top-width: 0px;
	border-bottom-width: 0px; */
	width: 100%;
}

.elemOfScrollBar {
	margin-left: 20px;
  display: flex;
  align-items: center;
  flex-direction: column;
	min-width: 140px;
}

.blockImg {
  position: relative;
}

.img {
  border-radius: 100%;
  width: 105px;
  height: auto;
}

.name {
  color: #fff;
  font-size: 30px;
  text-align: center;
}

#blockToReplyInvitation {
	display: flex;
	justify-content: space-between;
	padding: 0px 8px;
	box-sizing: border-box;
	position: absolute;
	width: 100%;
	left: 0px;
	top: 80px
}

.btn {
  background-color: rgb(61, 206, 102);
  position: relative;
  width: 25px;
  height: 25px;
	border-radius: 15px;
}

.plus::before,
.plus::after {
  position: absolute;
  background-color: rgb(255, 255, 255);
  width: 14px;
	border-radius: 2px;
	top: 50%; margin-top: -1.25px;
  left: 50%; margin-left: -7px;
	height: 2.5px;
	content: '';
	display: block;
	transition: .2s;
}

.plus::after {
	transform: rotate(90deg);
}

.minus::before,
.minus::after {
  position: absolute;
  background-color: rgb(255, 255, 255);
	top: 50%; margin-top: -1px;
  left: 50%; margin-left: -7px;
  height: 2.5px;
	border-radius: 2px;
	width: 14px;
	content: '';
	display: block;
	transition: .2s;
}.minus::after {
	transform: rotate(45deg);
}.minus::before {
	transform: rotate(-45deg);
}

.btn:hover .minus::after {
	transform: rotate(45deg) scaleX(1.2);
} .btn:hover .minus::before {
	transform: rotate(-45deg) scaleX(1.2);
}

.btn:hover .plus::after {
	transform: rotate(90deg) scaleX(1.2);
} .btn:hover .plus::before {
	transform: scaleX(1.2);
}

.btn:hover {
	transition: .2s;
	transform: translateY(-2px);
}

#numOfMissed {
	font-size: 14px;
	justify-content: center;
	align-items: center;
	position: absolute;
	display: flex;
	padding: 2px;
	box-sizing: border-box;
	min-width: 25px;
	width: fit-content;
	height: 25px;
	border-radius: 15px;
	top: 0px;
	left: 5px;
	background-color: rgb(243, 75, 75);
	color: #fff;
}

#scrollBar::-webkit-scrollbar {
	height: 0px;
}

</style>
<template>
	<div>
			<div v-if="setType != 'userBlocked'">
				<button v-if="setType != null" @click="sendRequest('blocked')" class="blocked colorBtnRed" >Blocked</button>
				<div v-if="setType == 'friendInvitation'" class="btnsRejectAndAccept">
						<button @click="sendRequest('reject')" class="blocked colorBtnRed " >Reject</button>
						<button @click="sendRequest('accept')" class="blocked colorBtnGreen " :style="{'margin-top': '2%'}" >accept</button>
				</div>
				<div v-else-if="setType == 'user' ||  setType == 'friendshipRequest'" class="btnsRejectAndAccept">
						<button @click="sendRequest('add')" class="add" :class="{'colorBtnGreen thrid': setType == 'user'}">add</button>
				</div>
				<div v-else-if="setType == 'friend'" class="btnsRejectAndAccept">
						<button @click="sendRequest('delete')" class="blocked colorBtnRed ">delete</button>
				</div>
			</div>
			<div v-else>
				<button @click="sendRequest('unblocked')" class="blocked colorBtnGreen ">restore</button>
			</div>
	</div>
</template>


<script>

import axios from 'axios'

export default {
	inject: ['getTocken'],
	props: ['setId', 'setType'],
	emits: ['getType'],
	mounted() {
	},
	data() {
		return {
			oldTypeUser: null,
		}
	},
	methods: {
		sendRequest(typeRequest) {
			axios({
				method: 'post',
				url: '/api/world/users/' + this.setId + '/' + typeRequest,
				headers: {
					'Authorization': `Basic ${this.getTocken()}`
				},
			}).then((response) => {
				this.$emit('getType', response.data.profileSelectUser.type)
			})
		}
	},
	components: {}
}
</script>


<style scoped>

.btnsRejectAndAccept {
	width: 90px;
	margin-top: 2%;
	/* display: flex; */
}

.blocked {
	background-color: rgba(253, 112, 112, 0);
	border: 0;
	border-radius: 15px;
	font-family: UnicaOne;
	font-size: 20px;
	idth: 90px;
	height: 30px;
}

.add {
	/* background-color: #EC5656; */
	background-color: rgba(253, 112, 112, 0);
	border: 0;
	border-radius: 15px;
	font-family: UnicaOne;
	font-size: 20px;
	width: 50px;
	height: 30px;
	background-color: #838383;
}

.colorBtnGrey {
	border-color: #838383;
	color: #fff;
	background-color: #838383;
}

.colorBtnGrey:hover {
	background-color: #666565;
	transition: .3s;
	transform: translateY(-2px)
}

.colorBtnRed {
	color: #fff;
	background-color: #EC5656;
}

.colorBtnRed:hover {
	transition: .3s;
	background-color: #ff0000;
	transform: translateY(-2px)
}

.colorBtnGreen {
	border-color: #5bec56;
	color: #fff;
	background-color: #5bec56;
}

.colorBtnGreen:hover {
	background-color: #2ee628;
	transition: .3s;
	transform: translateY(-2px)
}

</style>
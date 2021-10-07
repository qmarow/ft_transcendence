<template>
	<div id="main">
		<div class="blockImageAndStatus">
			<img :class="status != null ? 'outline' : 'avatar'" :style="{'color': getColor()}"
				:src="image == undefined ? './../../images/image.svg' : require('./../../images/' + image)" />
			<span id="networkStatus" :style="{'color': getColor()}">{{(status == 'userBlocked') ? 'blocked' : status}}</span>
		</div>
		<span class="username">
			{{username}}
		</span>
	</div>
</template>


<script>
export default {
	props: ['username', 'image', 'status'],
	mounted() {
	},
	data() {
		return {}
	},
	methods: {
		getColor() {
			if (this.status == 'play') {
				return ('rgb(228, 230, 126)')
			} else if (this.status == 'online') {
				return ('rgb(71, 216, 83)')
			} else if (this.status == 'offline') {
				return ('rgb(219, 55, 55)')
			} else {
				return ('rgb(114, 114, 114)')
			}
		}
	}
}
</script>

<style scoped>

#main {
	position: relative;
	display: flex;
	flex-direction: column;
	align-items: center;
}

#networkStatus {
	position: absolute;
	left: 220px;
	font-weight: bold;
}

.blockImageAndStatus {
	/* display: flex; */
}

.status {
	color:rgb(114, 114, 114);
}

.username {
	color: #fff;
	font-size: 35px;
}

.outline {
	border: 5px solid;
	border-radius: 100%;
	margin-right: 18px;
	width: 242px;
	height: auto;
}

.avatar {
	border: 5px solid rgba(255, 254, 254, 0);
	border-radius: 100%;
	margin-right: 18px;
	width: 242px;
	height: auto;
}
</style>
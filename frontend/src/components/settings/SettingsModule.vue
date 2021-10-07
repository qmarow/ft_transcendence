<template>
  <div id="main">
    <div class="topBlock">
      <img class="image" src="./../../images/image.svg">
      <div class="blockUpload">
        <img  class="iconDown" src="./../../images/iconDownloud.svg" />
        <span class="uploadPhoto">Upload PHOto</span>
      </div>
    </div>
    <div class="blockAccount">
      <span class="txtAccount">Account</span>
      <div class="logIn">
        <span class="wordLog">LOGIN</span>
        <input v-model="login" style="margin-left: 61px" class="input inputLogin" :placeholder="userData.username"/>
      </div>
      <div class="passIn">
        <span  class="wordLog">PASSWORD</span>
        <input v-model="pass" style="margin-left: 13px" class="input inputLogin" placeholder="password"/>
      </div>
      <button @click="save()" class="btnNew">save</button>
    </div>
  </div>
  
</template>


<script>
import axios from 'axios'

export default {
  inject: ['getUserData', 'getTocken'],
  emits: ['getUserData'],
  props: {},
  mounted() {
    console.log("userData",);
  },
  data() {
    return {
      userData: this.getUserData(),
      login: '',
      pass: '',
    }
  },
  methods:  {
    save() {
      axios('/api/user/settings', {
        method: 'POST',
        headers: {
          'Authorization': `Basic ${this.getTocken()}`
        },
        data: {
					user: {
						username: this.login,
						password: this.pass,
            image: '',
					}
				}
      }).then((responce) => {
          this.$emit('getUserData', responce.data.profile)
          console.log(responce);
        })
    },
  },
  components: {}
}
</script>


<style scoped>

#main {
  padding-top: 72px;
  display: flex;
  flex-direction: column;
}

.topBlock {
  display: flex;
  align-items : center;
  flex-direction: column;
}
.blockUpload {
  display: flex;
  justify-content: center;
  width: 100%;
}

.blockAccount {
  margin-top: 100px;
  text-align: center;
}

.btnNew {
  background-color: rgba(47, 160, 223, 1);
  border-radius: 15px;
  width: 79px;
  height: 36px;
  border: 0;
  font-size: 20px;
  font-family: UnicaOne;
  transition: .2s;
  margin-top: 20px;
} .btnNew:hover {
  color: rgb(228, 228, 228);
  background-color: rgb(96, 182, 228);
  /* background-color: rgb(223, 47, 47); */
  transform:translateY(-1px)
}

.inputLogin {
  font-size: 30px;
  border-radius: 80px;
  background-color: rgba(68, 67, 67, 0.42);
  border: 0;

  width: 170px;
  height: 34px;
}

.wordLog {
  font-size: 26px;
  margin-top: 1%;
  color: #fff;
}

.logIn{
  margin-top: 7%;
  display: flex;
}

.passIn{
  margin-top: 3%;
  display: flex;
}

.txtAccount {
  font-size: 28px;
  color:rgb(255, 255, 255);
}

.iconDown {
  margin-top: 0.5%;
}

.uploadPhoto {
  font-size: 21px;
  color: rgb(255, 255, 255);
  margin-left: 0.5%;
}

.image {
  border-radius: 200px;
  width: 240px;
  height: 240px;
}

</style>
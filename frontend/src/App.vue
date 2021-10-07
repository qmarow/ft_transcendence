<template>
  <div id="mainApp">
    <router-view v-if="!auth"
      @sing="sing"
      @getDataUser="setDataUser"
      :userData="'data from App'"></router-view>
    <div v-else class="header">
      <div id="left-part-header">
        <button class="button">Play</button>
        <div class="elem"
          :class="activeModule == '/friends' ? 'active' : ''"
          @click="goToModule('/friends')"
          >
            friends
        </div>
        <div class="elem"
          :class="activeModule == '/world' ? 'active' : ''"
          @click="goToModule('/world')">
            world
        </div>
        <div class="elem"
          :class="activeModule == '/profile' ? 'active' : ''"
          @click="goToModule('/profile')">
            Profile
        </div>
        <div class="elem"
          :class="activeModule == '/ethers' ? 'active' : ''"
          @click="goToModule('/ethers')">
            ethers
        </div>
        <div class="elem"
          :class="activeModule == '/setting' ? 'active' : ''"
          @click="goToModule('/setting')">
            settings
        </div>
        <div class="elem"
          :class="activeModule == '/info' ? 'active' : ''"
          @click="goToModule('/info')">
            info
        </div>
      </div>
      <div id="right-part-header">
        <span @click="changeFlagWindowProfile()" class="nick" > {{userData.username}} </span>
        <img @click="changeFlagWindowProfile()" class="photo" src="./images/image.svg"/>
        <transition name="window-profile" >
          <div v-if="flagWindowProfile != 0" class="window-profile" :class="flagWindowProfile == 2 ? 'close': ''">
            <transition v-for="(elem, i) of 7" :key="i" name="elem-window-profile">
              <div v-if="arrIdentefierForElem[i] == true" class="elem-window-profile" @click="goToModule(arrPaths[i])">{{arrTitlesForPaths[i]}}</div>
            </transition>
          </div>
        </transition>
      </div>
      <div v-if="flagWindowProfile" @click="changeFlagWindowProfile()" id="closeWindowProfile"></div>
    </div>
    <div v-if="flagWindowProfile" @click="changeFlagWindowProfile()" id="closeWindowProfile"></div>
    <div v-if="auth" id="contentPage">
        <router-view @getUserData="setDataUser" v-if="auth"/>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      arrPaths: ['/friends', '/world', '/profile', '/ethers', '/setting', '/info','/auth'],
      arrTitlesForPaths: ['Friends','World', 'Profile', 'Ethers', 'Setting', 'Info', 'Exit'],
      arrIdentefierForElem: [],
      auth: true,
      userData: {begininValue: undefined},
      activeModule: null,
      url: this.$route.path,
      flagWindowProfile: 0,
    }
  },
  mounted(){
    console.log("APP");
    for(let i = 0; i < 7; i++) {
      this.arrIdentefierForElem.push(false);
    }
    console.log(sessionStorage);
    if (Object.prototype.hasOwnProperty.call(sessionStorage, "userData")) {
      this.userData = JSON.parse(sessionStorage.getItem('userData'));
    } else {
      sessionStorage.setItem('userData', "null");
    }
    if (!this.auth){
      this.$router.push('/auth')
    }
  },
  updated() {
    console.log("updated: ");
  },
  provide() {
    return {
      getTocken: this.getUserTocken,
      getUserData: this.getDataUser,
      goToModule: this.goToModule
    }
  },
  methods: {
    sing() {
      this.auth = true;
      this.$router.push('/info')
    },
    goToModule(path) {
      console.log(path);
      this.$router.push(path);
    },
    changeFlagWindowProfile() {
      console.log("flag:", this.flagWindowProfile)
      if (this.flagWindowProfile == 2) {
        this.flagWindowProfile = 0;
      } else {
        this.flagWindowProfile++;
      }
    },
    setDataUser(newUserData) {
      this.userData = newUserData;
    },
    getDataUser() {
      return this.userData;
    },
    getUserTocken() {
      return (this.userData.token)
    }
  },
  computed: {
  },
  components: {
  },
  watch: {
    $route (to){
      this.activeModule = to.path
      if (this.activeModule == '/reg' || this.activeModule == '/auth') {
        this.auth = false;
      }
    },
    flagWindowProfile: function() {
			if (this.flagWindowProfile == 1) {
				for (let i = 1; i - 1 < this.arrIdentefierForElem.length; i++) {
					setTimeout(() => {
						this.arrIdentefierForElem[i - 1] = true;
            console.log(i);
					}, i * 30)
				}
			} else if (this.flagWindowProfile == 2){
        console.log('!!!!!!!!');
				setTimeout(() => {
					this.flagWindowProfile = 0;
					}, 50 * this.arrIdentefierForElem.length)
				for (let i = 1; i < this.arrIdentefierForElem.length + 1; i++) {
					((j) => {
						setTimeout(() => {
              console.log()
              let tmp = this.arrIdentefierForElem.length - j;
							this.arrIdentefierForElem[tmp] = false;
						}, j * 30)
					})(i)
				}
			}
		},
    userData(newData) {
      sessionStorage.setItem('userData', JSON.stringify(newData));
      console.log("User data", this.userData);
    }
  },
}
</script>

<style scoped>

#closeWindowProfile {
  z-index: 9;
  top: 0px;
  left: 0px;
  /* font-size: 50px; */
  display: inline-block;
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(71, 61, 139, 0);
  color:deeppink;
}

.window-profile {
  background-color: #313132;
  border: 1px solid #968686;
  border-radius: 17px;
  position: absolute;
  top: 70px;
  /* left: 80%; */
  z-index: 12;
  width: 200px;
  height: 133px;
  transition: .6s;
}

.window-profile-enter-active {
  height: 0px;
}.window-profile-enter-to {
  height: 133px;
  transition: .5s;
}
/* .window-profile-leave {
  height:200px;
  transition: 5s;
  background-color: rgba(109, 73, 209, 0.418);
} */
/* .window-profile-leave-active {
  height: 200px;
  transition: 1s;
  background-color: rgba(73, 209, 125, 0.418);
} */

.close {
  transform: .1s;
  height: 0;
  border: 2px;
  transform: translateY(-10px)
}

.elem-window-profile {
  display: inline-block;
  /* background-color: dimgray; */
  color:#fef;
  margin-top: 4px;
  padding: 5px 20px;
  border-radius: 20px;
  transition: 0.2s;
}.elem-window-profile:hover {
  background-color: rgb(123, 187, 107);
  transform:translateX(5px);
}

.elem-window-profile-enter-active {
  opacity: 0;
}.elem-window-profile-enter-to {
    transition: 0.2s;
  transform: translateY(-10px);
  opacity: 0;
}

.elem-window-profile-leave-active {
  transform: translateY(-10px);
  opacity: .0;
}

.elem-window-profile:last-child:hover {
  background-color: rgb(255, 113, 113);
} 

.header {
  box-sizing: border-box;
  padding: 26px 30px 0px;
  background-color: #202020;
  width: 100%;
  position: fixed;
  height: 86px;
  z-index: 10;
}

#left-part-header {
  /* background-color: #EC5656; */
  height: 100%;
  float: left;
  display: flex;
  align-items: center;
}
#right-part-header {
  height: 100%;
  position: relative;
  /* background-color: #56c1ec; */
  display: flex;
  justify-content: right;
  align-items: center;
}

#mainApp {
  height: 100vh;
}

#contentPage {
  height: calc(100% - 86px);
  display: flex;
  justify-content: center;
  position: relative;
  top: 86px;
}

.photo {
  margin-left: 1%;
  width: 60px;
  width: 60px;
}

.nick {
  font-size: 33px;
  margin-left: 21%;
  color:rgb(255, 255, 255)
}

.back {
  background-color: #fef;
}


.button {
  display: inline-block;
  width: 100px;
  height: 43px;

  background: #2FA0DF;
  border-radius: 19px;
  border-width: 0;
  font-family: UnicaOne;
  font-style: normal;
  font-weight: normal;
  font-size: 26px;
  color: #000000;
} .button:hover{
  background: #EC5656;
}

.steps {
  position: relative;
}

.elem {
  margin-left: 30px;
  font-size: 34px;
  line-height: 40px;

  display: flex;
  align-items: center;
  color: #FFFFFF;
} .elem:hover {
  border: 3px solid; /* Параметры границы */
  border-top-width: 0;
  border-left-width: 0;
  border-right-width: 0;
  border-bottom-color: #EC5656;
}

.active {
  border: 3px solid; /* Параметры границы */
  border-top-width: 0;
  border-left-width: 0;
  border-right-width: 0;
  border-bottom-color: #EC5656;
}


</style>

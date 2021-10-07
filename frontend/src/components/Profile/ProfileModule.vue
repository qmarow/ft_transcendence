<template>
  <div id="main">
    <div class="topBlock">
      <div class="avatarBlock">
        <avatar-block :username="profile.username" :image="profile.image" :status="(typeUser == 'userBlocked') ? 'blocked' : status"/>
      </div>
      <div v-if="typeUser != 'userBlocked'" class="statisticBlock">
        <span class="statistic">Statistic</span>
        <div class="topBlockInStatistic">
          <div class='blockGames'>
            <span class="games">Games {{profile.countGames}}</span>
            <svg :style="getStyleScale()" />
            <div class="numbersScale">
              <span class="numberWin">WIN {{profile.countWin}}</span>
              <span class="numberLose">Lose {{profile.countLose}}</span>
            </div>
          </div>
          <div class="blockRating">
            <div id="rating">
              <span class="games">Rating {{profile.rating}}</span>
              <img class="cup" src="./../../images/iconCup.svg" />
            </div>
            <div :style="{'display': 'flex'}">
              <span class="numberRating Min">Min  {{profile.minimalRating}}</span>
              <span class="numberRating Max">Max  {{profile.maximumRating}}</span>
            </div>
          </div>
        </div>
        <div class="bottomBlockInStatistic">
          <div class="blockGames">
            <span class="strBestWinStreak">Best Win streak</span>
            <div class="num8_fire">
              <span class="number">{{profile.bestWinStreak}}</span>
              <img class="fire" src="./../../images/iconFire.svg" />
            </div>
          </div>
          <div class="blockRating">
             <span class="strBestWin">Best Win</span>
            <div class="num8_fire">
              <span class="number">{{profile.bestWin}}</span>
              <img class="bestCup" src="./../../images/iconCupBestWin.svg" />
            </div>
          </div>
        </div>
      </div>
      <div class="buttonBlock">
        <!-- <router-view></router-view> -->
        <BlockButton @getType="changeType" :setId="profile.id" :setType="typeUser"/>
      </div>
    </div>
    <div v-if="typeUser != 'userBlocked'" class="bottomBlock">
      <span class="strHistoryFights">History Fights</span>
      <div class="headerHistory">
        <span class="header" :class="'positionApponent'">Apponent</span>
        <span class="header" :class="'positionScore'">Score</span>
        <span class="header" :class="'positionMe'">Me</span>
        <span class="header" :class="'positionData'">Data</span>
      </div>
      <ul class="listHistory">
        <li v-for="elem in profile.history" :key="elem.id" class="elemList" :class="getColor(elem)">
          <span class="wordList" :class="'apponent'">{{elem.apponent}}</span>
          <div class="wordList" :class="'score'">
            <div class="goalsApponent">
              {{elem.goalsApponent}}
            </div>:
            <div class="goalsUser">
              {{elem.goalsUser}}
            </div>
          </div>
          <div class="user">
            <span class="wordList">{{elem.user}}</span>
          </div>
          <div class="data">
            <span>{{elem.data}}</span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>


<script>

import axios from 'axios'
import AvatarBlock from "./avatarBlock.vue"
import BlockButton from "./blockButton.vue"

export default {
  props: {},
  inject: ['getTocken'],
  updated() {
  },
  mounted() {
    this.sendRequest();
  },
  data() {
    return {
      profile: {
        id: 1,
        username: 'Qmarowak',
        image: 'image.svg',
        countGames: 1000,
        countWin: 801,
        countLose: 199,
        bestWinStreak: 5,
        rating: 200,
        minimalRating: 150,
        maximumRating: 250,
        bestWin: 265,
        history: [
          {
            id: 1,
            user: 'qmarowak',
            apponent: 'utoomey',
            goalsUser: 15,
            goalsApponent: 10,
            data: "1 Dec 2012",
          },
          {
            id: 2,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 5,
            goalsApponent: 7,
            data: "21 Feb 2002",
          },
          {
            id: 3,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 5,
            goalsApponent: 7,
            data: "21 Feb 2002",
          },
          {
            id: 4,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 5,
            goalsApponent: 7,
            data: "21 Feb 2002",
          },
          {
            id: 5,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 56,
            goalsApponent: 7,
            data: "21 Feb 2002",
          },
          {
            id: 6,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 5,
            goalsApponent: 7,
            data: "21 Feb 2002",
          },
          {
            id: 7,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 51,
            goalsApponent: 7,
            data: "1 Feb 2002",
          },
          {
            id: 8,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 5,
            goalsApponent: 72,
            data: "21 Feb 2002",
          },
          {
            id: 9,
            user: 'ninja',
            apponent: 'stalit',
            goalsUser: 115,
            goalsApponent: 72,
            data: "2 Feb 2022",
          },
          {
            id: 10,
            user: 'Op-hey-lalaly',
            apponent: 'Op-hey-lalaly',
            goalsUser: 5,
            goalsApponent: 72,
            data: "21 Feb 2002",
          },
          {
            id: 11,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 5,
            goalsApponent: 72,
            data: "21 Feb 2002",
          },
          {
            id: 12,
            user: 'qmarowak',
            apponent: 'hballaba',
            goalsUser: 5,
            goalsApponent: 72,
            data: "21 Feb 2002",
          }
        ]
      },
      typeUser: null,
      status: null,
    }
  },
  provide() {
    return {
    getType: this.getType,
    getId: this.getId,
    }
  },
  methods: {
    getColor(elem) {
      if (elem.goalsUser - elem.goalsApponent < 0) {
        return 'colorLose';
      }
      return 'colorWin';
    },
    getType() {
      return (this.typeUser);
    },
    changeType(newType) {
      this.typeUser = newType;
    },
    getId() {
      return (this.profile.id);
    },
    getStyleScale() {
      var percentWin = (this.profile.countGames > 0) ? 100 * this.profile.countWin / this.profile.countGames : 50;
      
      // console.log("count win", this.profile.countWin)
      return ({
        'width': '80%',
        'height': '10px',
        'border-radius': '30px',
        'margin': '0px',
        'margin-top': '10px',
        'background': `linear-gradient(90deg, #37C35E ${percentWin}%, #DB4141 ${percentWin}%)`,
      })
    },
    sendRequest() {
      let urlAddres = this.$route.path;
      console.log("urlAdress", urlAddres)
      
      if (urlAddres == '/profile') {
        urlAddres = '/api/user/profile'
      } else {
        urlAddres = '/api/world/users/' + urlAddres.substr(13);
      }
      axios({
        method: 'get',
        url: urlAddres,
        headers: {
          'Authorization': `Basic ${this.getTocken()}`
          }
      }).then(response => {
        this.updateData(response);
      }).catch(response => {
        console.log(response)
      })
    },
    updateData(response) {
      // let tmpHistory = this.profile.history;
      if (response.data.profile == undefined) {
        this.profile = {...response.data.profileSelectUser}
        this.status = this.profile.status
        this.typeUser = this.profile.type;
        console.log("Type: ", this.typeUser)
      } else {
        this.profile = {...response.data.profile}
        this.typeUser = null
        this.status = null;
        console.log("$$$$$$$$")
      }
      // console.log("Position:",this.profile.position);
      if (this.profile.image === '') {
        this.profile.image = 'image.svg'
      }
      // this.profile.history = tmpHistory;
      console.log('Type user:', this.typeUser);
      console.log('Status:', this.status);
    }
  },
  computed: {
  },
  watch: {
    $route: function() {
      console.log("!!!!!!!!");
      this.sendRequest();
    }
  },
  components: {
    AvatarBlock: AvatarBlock,
    BlockButton: BlockButton,
  }
}
</script>

<style scoped>

#main {
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  height: 100%;
  padding-top: 41px;
}

.buttonBlock {
  width: 200px;
  height: 294px;
  box-sizing: border-box;
}

.colorLose {
  color:rgb(223, 172, 172);
  background-color: rgba(219, 65, 65, 0.26);
}

.colorWin {
  background-color: rgba(55, 195, 94, 0.26);
  color:rgb(172, 223, 172);
}

.data {
  margin-left: 22%;
  width: 195px;
  text-align: right;
}

.goalsUser {
  width: 50px;
  text-align: left;
}

.goalsApponent {
  /* background-color: aquamarine; */
  width: 50px;
  text-align: right;
}

.user {
  margin-left: 12.6%;
  /* background-color: rgb(58, 184, 184); */
  width: 200px;
}

.score {
  margin-left: 6.2%;
}

.apponent {
  margin-left: 3.6%;
  /* background-color: antiquewhite; */
  width: 210px;
}

.wordList {
  /* color: #fff; */
  display: flex;
  font-size: 28px;
}

.elemList {
  opacity: .5s;
  width: 1298px;
  height: 70.12px;

  margin-top: 3px;

  align-items: center;

  font-size: 28px;
  display: flex;
}

.listHistory::-webkit-scrollbar {
  width: 0px;
  /* background-color: #606061;
  border-radius: 1000px; */
}

/* .listHistory::-webkit-scrollbar-thumb {
  border-radius:1000px;
  background-color: #2e2e2e;
}

.listHistory::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.2);
  border-radius: 100px;
  background-color: #606061;
} */

.listHistory {
  height: fit-content;
  overflow: auto;
  margin-block-end: 0px;
}

.positionApponent {
  margin-left: 3.5%;
}

.positionScore {
  margin-left: 14.7%;
}

.positionMe {
  margin-left: 16.5%;
}

.positionData {
  margin-left: 41.3%;
}

.header {
  font-size: 32px;
  color: #fff;
}

.headerHistory {
  /* background-color: darksalmon; */
  display: flex;
  width: 100%;
  margin-block-end: 0px;;
}

.strHistoryFights {
  /* background-color:brown; */
  color: #fff;
  font-size: 38px;
}

.bottomBlock {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: calc(100% - 320px);
  min-height: 265px;
  box-sizing: border-box;
}

.bestCup {
  width: 60px;
  height: 60px;
}

.number {
  font-size: 50px;
  color: #fff;
}

.strBestWin {
  font-size: 28px;
  color: #fff;
}

.num8_fire {
  width: 100%;
  height: 60px;
  display: flex;
  justify-content: center;
}

.fire {
  width: 60px;
  height: 60px;
}


.strBestWinStreak {
  font-size: 28px;
  color: #fff;
}

.bestWinStreak {
  text-align: center;
}

.Max {
  margin-left: 50px;
}

.numberRating {
  margin-top: 2%;
  font-size: 25px;
  color: #fff;
}

#rating {
  display: flex;
  align-items: center;
}

.cup {
  width: 25px;
  height: 25px;
}

.blockRating {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50%;
}

.numberWin {
  color: #93FF82;
  font-size: 17px;
}

.numberLose {
  color: #DB4141;
  font-size: 17px;
  /* margin-left: 61%; */
}

.numbersScale {
  display: flex;
  justify-content: space-between;
  width: 80%;
}

.games {
  font-size: 30px;
  color: rgb(255, 255, 255);
  /* background-color: cornsilk; */
}

.blockGames {
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.topBlockInStatistic {
  width: 100%;
  height: 120px;
  display: flex;
}

.bottomBlockInStatistic {
  /* background-color: rgb(187, 121, 173); */
  margin-top: 1%;
  width: 100%;
  height: 120px;
  display: flex;
}

.statistic {
  font-size: 38px;
  margin-left: 42%;
  color:rgb(255, 255, 255)
}

.statisticBlock {
  width: 800px;
}

.avatarBlock {
  width: 320px;
}

.topBlock {
  box-sizing: border-box;
  display: flex;
}

@media (max-width: 1350px) {

}

</style>

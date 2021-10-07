<template>
  <div class="blockWorld">
    <input class='input search' v-model="stringSearch" placeholder="search friends"/>
    <ul class="list">
      <li class="input itemList" v-for="(elem, i) in ethers"
        v-show="filterByWord(elem)"
        :key="i">
        <div class="time">
          {{elem.duration}}
        </div>
        <div class="revals">
          <div class="user1">
            {{elem.firstFighter}}
          </div>
          <div>
            <img src="./../../images/iconFight.svg" />
          </div>
          <div class="user2">
            {{elem.secondFighter}}
          </div>
        </div>
        <div class="countWatching">
          {{elem.numberOfWatching}}
        </div>
        <div>
          <img src="./../../images/iconEye.svg" />
        </div>
      </li>
    </ul>
  </div>
</template>


<script>
import axios from 'axios'

export default {
  props: {},
  inject: ['getTocken'],
  mounted() {
    axios({
      method: 'get',
			url: '/api/ethers',
			headers: {
				'Authorization': `Basic ${this.getTocken()}`
			},
    }).then((response) => {
      console.log(response.data.ethers[1]);
      this.ethers = [...response.data.ethers]
      console.log("ethers:", this.ethers[1].id);
    })
  },
  data() {
    return {
      stringSearch: '',
      ethers: [
        {
          id: 1,
          firstFighter: 'qmarowak',
          secondFighter: 'utoomey',
          duration: 200,
          numberOfWatching: 5,
        }
      ]
    }
  },
  methods: {
    // getTime(time) {
    //   var hour = Math.trunc(time / 3600);
    //   var remainderMinut = time - hour * 3600;
    //   var minut = Math.trunc((time - hour * 3600) / 60);
    //   var second = remainderMinut - (minut * 60);
      

    //   hour = (Math.ceil(Math.log10(hour + 1)) <= 1) ? '0' + hour : hour;
    //   minut = (Math.ceil(Math.log10(minut + 1)) <= 1) ? '0' + minut : minut;
    //   second = (Math.ceil(Math.log10(second + 1)) <= 1) ? '0' + second : second;
    //   return (hour + ':' + minut + ':' + second);
    // },
    filterByWord(id) {
      let rivalOneMin = id.firstFighter.toLowerCase();
      let rivalOneMax = id.firstFighter.toUpperCase();
      let rivalTwoMin = id.secondFighter.toLowerCase();
      let rivalTwoMax = id.secondFighter.toUpperCase();

      for (var i = 0; this.stringSearch[i]; ++ i) {
        if (rivalOneMin[i] != this.stringSearch[i] 
          && rivalOneMax[i] != this.stringSearch[i]
          && rivalTwoMin[i] != this.stringSearch[i]
          && rivalTwoMax[i] != this.stringSearch[i]) {
          return false;
        }
      }
      return id
    }
  },
  components: {}
}
</script>

<style scoped>

.countWatching {
  font-size: 20px;
  margin-left: 20%;
  width: 40px;
  text-align: right;
}

.user1 {
  margin-top: 2%;
  margin-right: 5%;
  margin-left: 5%;

  width: 130px;
  text-align: right;
}

.user2 {
  margin-top: 2%;
  margin-right: 5%;
  margin-left: 5%;

  width: 130px;
}

.revals {
  display: flex;
  margin-top: 0.4%;
  margin-left: 16.5%;
  width: 400px;
}

.time {
  margin-left: 2%;
  margin-bottom: 0.3%;
  width: 70px;
  font-size: 17px;
}

.blockWorld {
  max-height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 45px;
  padding: 0px;
}


.list {
  width: 920px;
  /* height: 100%; */
  overflow: auto;
  margin-block-end: 0px;
  margin-block-start: 0px;
  margin-top: 14px;
}

.list::-webkit-scrollbar {
  margin-left: 0px;
  width: 6px;
  background-color: #606061;
  border-radius: 1000px;
}

.list::-webkit-scrollbar-thumb {
  border-radius:1000px;
  background-color: #2e2e2e;
}

.list::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.2);
  border-radius: 100px;
  background-color: #606061;
}

.itemList {
  opacity: .5s;
  width: 893px;
  height: 43.86px;
  border-radius: 20px;

  margin-top: 0.6%;

  display: flex;
  align-items: center;

  text-align: left;
  padding-top: 0.5%;
  font-size: 26px;
}

.search {
  font-size: 28px;
  
  width: 632px;
  min-height: 49px;

  border-radius: 17px;
  text-align: left;
  
  background-image: url('./../../images/freeIconFind.png');
  background-repeat: no-repeat;
  padding-left: 67px;
  background-position-x: 20px;
  background-position-y: 45%;
  background-size: 4%;
}
</style>
<template>
  <div id="main">
    <text class="trunc">ft_transcendence</text>
      <div class="text">
          <span class="headwords">AbouT project:</span> ft_transcendens a 
          <p>project in which it was necessary to make a </p>
          <p>site where you can play pong, chat with </p>
          <p>friends</p>
      </div>
      <div class="text">
          <span class="headwords">rules of the game:</span> ft_transcendens a 
          <p>project in which it was necessary to make a </p>
          <p>site where you can play pong, chat with </p>
          <p>friends</p>
      </div>
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
      url: '/api/descriptions',
      headers: {
        'Authorization': `Basic ${this.getTocken()}`
      }
    }).then((responce) => {
      console.log("!!",responce);
    })
  },
  data() {
    return {}
},
  components: {}
}
</script>


<style scoped>

#main {
  width: fit-content;
  /* background-color: #308d4f; */
  display: flex;
  flex-direction: column;
}

.headwords {
  color: #E2CF8D;
  font-size: 64px;
}

.text {
  font-size: 36px;
  color:rgb(255, 255, 255);
}

.trunc {
  /* background-color: aqua; */
  font-style: normal;
  font-weight: normal;
  font-size: 144px;
  /* letter-spacing: -0.03em; */

  color: #7663EF;
}
</style>
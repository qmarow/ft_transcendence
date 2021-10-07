<template>
  <div id='main'>
    <div class="blockScrollBar">
      <ScollBar
        :typeActive="typeActive"
        :data="(typeActive == 'chats') ? chats : friends"
        @getActive="changeActive"
        @createChat="chat"
        @selectedChat="setSelectedChat"/>
    </div>
    <div id="chatModule">
      <ChatModule :dataChat="selectedChat"/>
    </div>
    <div @click="changeWinCreateChat(-1)" v-if="activeWinCreateChat > 0" id="WindowCreateChat">
      <WindowCreateChat @click="changeWinCreateChat(1)"  @getData="setData"/>
    </div>
  </div>
</template>


<script>
import ScrollBar from "./scrollBarFriendsAndChats.vue"
import WindowCreateChat from './WindowCreateChat.vue'
import ChatModule from "./ChatModule.vue"
export default {
  props: {},
  data() {
    return {
      typeActive: 'chats',
      activeWinCreateChat: 0,
      selectedChat: null,
      chats: [
        {
          id: 1,
          name: 'cool team',
          images: 'images/image.svg',
          numberOfMissed: 10,
          status: 'online',
          type: 'chat',
        },
        {
          id: 2,
          name: 'cool team',
          images: 'images/image.svg',
          numberOfMissed: 0,
          status: 'online',
          type: 'chatOpen',
        },
        {
          id: 3,
          name: 'cool team',
          images: 'images/image.svg',
          numberOfMissed: 10,
          status: 'paly',
          type: 'chatBlocked',
        },
        {
          id: 4,
          name: 'cool team',
          images: 'images/image.svg',
          numberOfMissed: 10,
          status: 'offline',
          type: 'friendInvitation',
        }
      ],
      friends: [
        {
          id: 1,
          name: 'qmarowal',
          images: 'images/image.svg',
          numberOfMissed: 10,
          status: 'online',
          type: 'chat',
        },
        {
          id: 2,
          name: 'Stalit',
          images: 'images/image.svg',
          numberOfMissed: 0,
          status: 'online',
          type: 'chatOpen',
        },
        {
          id: 3,
          name: 'Petr I',
          images: 'images/image.svg',
          numberOfMissed: 10,
          status: 'paly',
          type: 'chatBlocked',
        },
        {
          id: 4,
          name: 'Ybiv0',
          images: 'images/image.svg',
          numberOfMissed: 10,
          status: 'offline',
          type: 'friendInvitation',
        },
        {
          id: 4,
          name: 'TonyCark',
          images: 'images/image.svg',
          numberOfMissed: 10,
          status: 'offline',
          type: 'friendInvitation',
        },
        {
          id: 4,
          name: 'Oby One',
          images: 'images/image.svg',
          numberOfMissed: 10,
          status: 'offline',
          type: 'friendInvitation',
        }
      ],
    }
  },
  methods: {
    changeActive(changedActive) {
      console.log("typeActive:", changedActive)
      this.typeActive = changedActive;
    },
    setData(data) {
      console.log(data);
      this.activeWinCreateChat = 0;
    },
    chat() {
      console.log('$$$$$$');
      this.activeWinCreateChat = 1;
    }, 
    setSelectedChat(selectedChat) {
      this.selectedChat = selectedChat;
    },
    changeWinCreateChat(a) {
      this.activeWinCreateChat += a;
    }
  },
  components: {
    ScollBar: ScrollBar,
    WindowCreateChat: WindowCreateChat,
    ChatModule: ChatModule,
  }
}
</script>


<style scoped>

.blockScrollBar {
  width: 100%;
  height: 120px;

  margin-left: 0.5%;
  margin-top: 2%;
}

#main {
  padding-top: 10px;
}

#WindowCreateChat {
  display: flex;
  justify-content: center;
  align-items: center;
  top: 0px;
  left: 0pc;

  z-index: 11;
  position: fixed;
  width: 100vw;
  height: calc(100vh + 1px);
  background-color: rgba(37, 37, 37, 0.336);
}

#chatModule {
  margin-top: 62px
}

</style>
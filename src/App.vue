<template>
  <div id="app">
    <msg-list :globalData="globalData"></msg-list>
    <add-msg class="inputArea"></add-msg>
  </div>
</template>

<script>
import MsgList from './components/msgList/Index'
import AddMsg from './components/AddMsg'

export default {
  name: 'App',
  components: {
    MsgList,
    AddMsg
  },
  data(){
    return{
      globalData: {
        userId: 'self',
        userStyle: {
          fontColor: '#fff',
          fontSize: '16px'
        },
        userBackgroundColor: '#fcd6dc'
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
}
*{
  margin: 0;
  padding: 0;
}
li{
  list-style: none;
}
.inputArea{
  position: absolute;
  bottom: 0;
  left: 0;
}
.clearfix::after{
  content: '';
  display: block;
  clear: both;
}
</style>

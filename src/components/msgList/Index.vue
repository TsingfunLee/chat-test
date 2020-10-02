<template>
    <div class="msgListWrap" :style="{backgroundColor: globalData.userBackgroundColor}">
        <ul class="msgList">
            <li class="msgItem" v-for="(item ,i) in msgList" :key="i">
                <div :class="['bubbleMsg', 'clearfix', globalData.userId == item.userId ? 'self' : '']" v-if="item.type != 'sysInfo'">
                    <div class="avatar">                    
                    </div>
                    <div class="bubble">
                        <text-msg v-if="item.type == 'txt'" :content="item.content" :msgStyle="item.style"></text-msg>
                        <image-msg v-if="item.type == 'img'" :url="item.url"></image-msg>                       
                    </div>              
                </div>
                <div v-else class="tipMsg">
                    <sys-info :content="item.content"></sys-info>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
import TextMsg from './TextMsg'
import ImageMsg from './ImageMsg'
import SysInfo from './SysInfo'

export default {
    name: 'messegeList',
    components: {
        TextMsg,
        ImageMsg,
        SysInfo
    },
    props: {
        globalData: Object
    },
    data(){
        return {
            msgList:[{
                type: 'sysInfo',
                content: 'You have already became freind.'
            },{
                type: 'img',
                userId: 'default',
                url: "./1.jpg"
            },{
                type: 'txt',
                userId: 'default',
                content: 'Hey, nice to meet you.',
                style: {
                    fontColor: '#000000',
                    fontSize: '14px'
                }
            }]
        }
    },
    created(){
        this.$bus.$on('send', (msg)=>{
            this.msgList.push({
                type: 'txt',
                userId: 'self',
                content: msg,
                style: this.globalData.userStyle
            })
        })
        this.$bus.$on('upload', (msg)=>{
            this.msgList.push({
                type: 'img',
                userId: 'self',
                url: msg
            })
        })
    }
}
</script>

<style scoped>
.msgListWrap{
    padding-top: 30px;
    padding-left: 15px;
    padding-right: 15px;
    padding-bottom: 40px;
    box-sizing: border-box;
    height: 100vh;
    overflow: scroll;
}
.msgItem{
    margin-bottom: 15px;
}
.bubbleMsg{
    white-space: nowrap;
}
.avatar{
    width: 40px;
    height: 40px;
    border-radius: 100%;
    background-color: paleturquoise;
    display:inline-block;
}
.bubble{
    width: auto;
    height: auto;
    padding: 10px;
    background-color: papayawhip;
    border-radius: 0px 5px 15px 5px;
    position: relative;
    display: inline-block;
    margin-left: 10px;
    margin-top: 15px;
    vertical-align: top;
    max-width: calc(100vw - 130px);
    box-sizing: border-box;
}
.bubble::before{
    content: '';
    display: block;
    width: 0;
    height: 0;
    border-style: solid;
    border-width: 5px;
    border-top-color: papayawhip;
    border-left-color: transparent;
    border-right-color: transparent;
    border-bottom-color: transparent;
    position: absolute;
    top: 0px;
    left: -5px;
}
.bubbleMsg.self .avatar{
    float:right;
    background-color: goldenrod;
}
.bubbleMsg.self .bubble{
    float: right;
    margin-right: 10px;
    border-radius: 5px 0px 5px 15px;
    background-color: skyblue;
}
.bubbleMsg.self .bubble::before{
    left: unset;
    right: -5px;
    border-top-color: skyblue;
}
.tipMsg{
    display: inline-block;
    padding: 5px;
    background-color: #cccccc;
    color: white;
    border-radius: 2px;
    font-size: 12px;
    transform: translateX(-50%);
    position: relative;
    left: 50%;
}
</style>
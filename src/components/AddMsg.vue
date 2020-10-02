<template>
    <div class="addMsgWrap">
        <input class="input" v-model="msg" placeholder="Please input messege" type="text">
        <div class="uploadImgBtn">          
            <div class="imgBtn"></div>
            <input class="uploadImg" type="file" name="image" @change="uploadImg">
        </div>       
        <button class="send" type="button" @click="send">Send</button>
    </div>
</template>

<script>
export default {
    name: 'addMsg',
    props: {

    },
    data(){
        return{
            msg: '',
            url: ''
        }
    },
    methods: {
        send(){
            this.$bus.$emit('send', this.msg)
            this.msg = ''
        },
        uploadImg(e){
            let file = e.target.files[0]
            let fr = new FileReader()
            fr.onload = (e) => {
                this.url = e.target.result
                this.$bus.$emit('upload', this.url)
            }
            if(/.jpg|.png|.jpeg/.test(file.name)){
                fr.readAsDataURL(file)
            }else{
                alert('File format only support: jpg/jpeg/png')
            }           
        }
    }
}
</script>

<style scoped>
.addMsgWrap{
    width: 100%;
    background: palegoldenrod;
    height: 40px;
    box-sizing: border-box;
    padding: 5px;
    display: flex;
    justify-content: space-between;
}
.input{
    height: auto;
    border-radius: 5px;
    border: none;
    outline: none;
    padding: 0 5px;
}
.send{
    border: none;
    background-color: white;
    border-radius: 2px;
    padding: 0 4px;
    outline: none;
    color: goldenrod;
}
.uploadImgBtn{
    position: relative;
}
.uploadImg{
    opacity: 0;
    width: 30px;
    height: 30px;
}
.imgBtn{
    width: 30px;
    height: 30px;
    border-radius: 100%;
    background-color: white;
    position: absolute;
    top: 0;
    left: 0;
}
.imgBtn::before{
    content: '';
    display: block;
    width: 20px;
    height: 2px;
    background-color: goldenrod;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
.imgBtn::after{
    content: '';
    display: block;
    width: 2px;
    height: 20px;
    background-color: goldenrod;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
</style>    
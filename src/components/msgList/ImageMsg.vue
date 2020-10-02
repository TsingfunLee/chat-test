<template>
    <div>
        <img :src="url" alt="img" class="img">
    </div>
</template>

<script>
export default {
    name: 'imageMsg',
    props:{
        url: String
    }
}
</script>

<style scoped>
.img{
    width: 100px;
    height: auto;
}
</style>
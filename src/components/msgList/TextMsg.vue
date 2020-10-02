<template>
    <div class="text" :style="{fontSize: msgStyle.fontSize, color: msgStyle.fontColor}">
        {{content}}
    </div>
</template>

<script>
export default {
    name: 'textMsg',
    props: {
        content: String,
        msgStyle: Object
    }
}
</script>

<style scoped>
.text{
    white-space: normal;
    word-break: break-all;
}
</style>
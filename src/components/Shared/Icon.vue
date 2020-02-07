<template>
    <div class="icon-wrapper">
        <img class="character-icon abs-center" :src="iconDateBase64" alt="icon" :style="IMGstyle" />
    </div>
</template>

<script>
    export default {
        name: "Icon",
        props: {
            iconDateBase64: String,
            IMGstyle: String
        },
        mounted() {
            console.log("Icon mounted")
        },
        data() {
            return {}
        },
        computed: {}
    }
</script>

<style scoped>
    .icon-wrapper {
        background: $avatarBackground;
        height: 200px;
        width: 200px;
        border-radius: 50%;
        position: relative;
        overflow: hidden;
    }
    .icon-wrapper img {
        max-height: 100%;
    }
</style>
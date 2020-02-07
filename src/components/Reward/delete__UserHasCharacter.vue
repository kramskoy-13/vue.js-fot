<template>
    <div class="user-character">
        <Icon :iconDateBase64="charachterAvatar" />

        <div class="user-character__icon-wrapper">
            <img src="../../assets/newMessage.svg" alt="user message" />
            <p class="user-character__text">Alex краще 78%!</p>
        </div>
    </div>
</template>

<script>
    import Icon from "../Shared/Icon.vue";

    export default {
        name: "UserHasCharacter",
        components: { Icon },
        props: {
            charachterAvatar: String,
            charachterName: String
        },
        mounted() {
            console.log("User Has Character mounted")
        },
        data() {
            return {}
        },
        computed: {}
    }
</script>

<style scoped>
    .user-character {
        display: flex;
        justify-content: center;
        position: relative;
    }
    .user-character__icon-wrapper {
        position: absolute;
        top: -15px;
        right: 0;
    }
    .user-character__text {
        position: absolute;
        top: 15px;
        left: 29px;
        font-weight: bold;
        font-size: 12px;
        line-height: 16px;
        color: #FFFFFF;
        text-align: left;
    }
</style>
<template>
    <div>
        <div v-if="userHasCharacter" class="user-character">
            <Icon :iconDateBase64="charachterAvatar" />

            <div class="user-character__icon-wrapper left">
                <img src="../../assets/newMessage.svg" alt="user message" />
                <p class="user-character__text">Alex краще 78%!</p>
            </div>
        </div>

        <div v-else class="user-character" @click="openCreateUserTab">
            <img src="../../assets/chooseCharacterIcon.svg" alt="choose character icon" />

            <!-- <div class="user-character__icon-wrapper right">
                    <img src="../../assets/chooseCharacterMessage.svg" alt="choose character message" />
                    <p class="user-character__text"></p>
                </div>-->
            <button class="main-btn user-character__create-btn">обрати персонажа</button>
        </div>
    </div>
</template>

<script>
    import Icon from "../Shared/Icon.vue";

    export default {
        name: "UserAvatar",
        components: { Icon },
        props: {
            achievementsNumber: Number,
            openCreateUserTab: Function,
            userHasCharacter: Boolean,
            charachterAvatar: String,
            charachterName: String
        },

        data() {
            return {}
        },
        mounted() {
            console.log("UserAvatar mounted")
        }
    }
</script>

<style scoped>
    .user-character {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        position: relative;
    }
    .user-icon__container {
        position: relative;
        text-align: center;
    }
    .user-character__create-btn {
        text-transform: uppercase;
        margin: 18px 0;
    }
    .user-character__icon-wrapper {
        position: absolute;
        top: -15px;
        left: 0;
    }
    /*.right {
        right: 0;
    }*/
    /*.left {
        left: 0;
    }*/
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
<template>
    <div @click="openCreateUserTab">

        <div class="no-user-icon__container">
            <img src="../../assets/chooseCharacterIcon.svg" alt="choose character icon" />

            <div class="no-user-character__icon-wrapper">
                <img src="../../assets/chooseCharacterMessage.svg" alt="choose character message" />
                <p class="no-user-character__text">Оберить персонажа</p>
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        name: "UserHasNoCharacter",
        props: {
            achievementsNumber: Number,
            openCreateUserTab: Function
        },
        components: {
            
        },
        data() {
            return {}
        },
        mounted() {
            console.log("UserHasNoCharacter mounted")
        }
    }
</script>

<style scoped lang='scss'>
    .no-user-icon__container {
        position: relative;
        text-align: center;
    }
    .no-user-character__icon-wrapper {
        position: absolute;
        top: -15px;
        right: 0;
    }
    .no-user-character__text {
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
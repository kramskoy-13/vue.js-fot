<template>
    <div class="achivements-icon__container">
        <img v-if="completed" src="../../assets/achivBackgroundCompleted.svg" alt="achiv background icon" />

        <img v-else src="../../assets/achivBackground.svg" alt="achiv completed background icon" />

        <div v-if="completed" class="achivements-icon__icon">
            <img src="../../assets/achivIconCompleted.svg" alt="achivements background icon" />
        </div>

        <div v-if="completed" class="achivements-icon__badge-done">
            <img src="../../assets/achivBadgeCompleted.svg" alt="achivements icon" />
        </div>
    </div>
</template>

<script>
    export default {
        name: "AchivementItem",
        props: {
            completed: Boolean
        },
        data() {
            return {}
        }
    }
</script>

<style scoped lang='scss'>
    .achivements-icon__container {
        position: relative;
    }

    .achivements-icon__icon {
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .achivements-icon__badge-done {
        position: absolute;
        right: -10px;
        top: 0px;
    }
</style>
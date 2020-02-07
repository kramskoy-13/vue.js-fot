<template>
    <div>
        <div v-if="modalOpen" class="preloader-wr" @click="handleOutsideClick">
            <div class="modal-wrapper" ref="myModal">
                <div class="modal-icon-wrapper">
                    <AchivementIcon :completed="activeAchivement.achievementTotalDays === activeAchivement.achievementCompletedDays" />
                </div>
                <div class="modal-achiv-name">
                    {{activeAchivement.achievementName}}
                </div>
                <div class="modal-progess">
                    Виконано: {{activeAchivement.achievementCompletedDays}} з {{activeAchivement.achievementTotalDays}}
                </div>
                <div class="modal-description">
                    {{activeAchivement.achievementDescription}}
                </div>
                <button @click="toggleModal" class="main-btn modal-button">OK</button>
            </div>
        </div>

        <div class="achivements__wrapper">
            <div class="achivements__container" v-for="(achiv, index) in achievements" :key="index" @click="showAchivementDescription(achiv)">

                <AchivementIcon :completed="achiv.achievementTotalDays === achiv.achievementCompletedDays" />

                <div class="achivements__name">
                    {{ achiv.achievementName }}
                </div>
                <ProgressBar class="achivements__progress-bar" :percantage="achiv.achievementCompletedDays === 0 ? 0 : achiv.achievementCompletedDays/achiv.achievementTotalDays*100" />
            </div>
        </div>
    </div>
    
</template>

<script>
    import ProgressBar from "../Shared/ProgressBar.vue"
    import AchivementIcon from "./AchivementIcon.vue"

    export default {
        name: "AchievementsList",
        props: {
            achievements: Array
        },
        components: {
            ProgressBar,
            AchivementIcon
        },
        data() {
            return {
                activeAchivement: null,
                modalOpen: false
            };
        },
        mounted() {
            console.log("AchievementsList mounted")
        },
        methods: {
            showAchivementDescription(achivement) {
                this.toggleModal()
                this.activeAchivement = achivement
            },
            toggleModal() {
                this.modalOpen = !this.modalOpen
            },
            handleOutsideClick(event) {
                const { target } = event
                if (!this.$refs.myModal || target === this.$refs.myModal || this.$refs.myModal.contains(target)) return 
                this.modalOpen = false
            }
        }
    }
</script>

<style scoped>
    .achivements__wrapper {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        margin-top: 20px;
    }
    .achivements__container {
        width: 30%;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .achivements__progress-bar {
        width: 100%;
        max-width: 75px;
    }
    .achivements__name {
        text-align: center;
    }
    .achivements__container:nth-of-type(1n+4) {
        margin-top: 30px;
    }
    .modal-wrapper {
        width: 90vw;
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: white;
    }
    .modal-icon-wrapper {
        margin: 40px 0 12px;
    }
    .modal-achiv-name {
        font-style: normal;
        font-weight: bold;
        font-size: 18px;
        line-height: 24px;
        color: $primaryColorActive;
    }
    .modal-progess {
        font-style: normal;
        font-weight: 600;
        font-size: 14px;
        line-height: 24px;
        color: $primaryTextColor;
        margin-bottom: 20px;
    }
    .modal-button {
        min-width: 220px;
        text-align: center;
        margin: 40px auto;
    }
    .modal-description {
        width: 90%;
        font-size: 16px;
        line-height: 24px;
        text-align: center;
        color: $secondaryTextColor;
    }
</style>
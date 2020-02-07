<template>
    <div class="user-progress">
        <!--<h3 class="user-progress__status">
            {{userStatus}}
        </h3>-->

        <p class="user-progress__description">
            {{userDescription}} 
        </p>
    </div>
</template>

<script>
    export default {
        name: "UserProgress",
        props: {
            achievements: Array,
            userStatus: String
        },
        mounted() {
            console.log("UserProgress mounted")
        },
        data() {
            return {}
        },
        computed: {
            numberOfCompletedAchivements() {
                let achievementsCompleted = this.achievements.filter(ac => ac.achievementTotalDays === ac.achievementCompletedDays)
                return achievementsCompleted.length
            },
            userDescription() {
                let completedAchievementsLength = this.numberOfCompletedAchivements
                let totalAchievementsLength = this.achievements.length

                return completedAchievementsLength === 0
                    ? `Виконуйте завдання та отримайте всі ${totalAchievementsLength} нагород!`
                    : `Ви успішно отримали ${completedAchievementsLength} нагород з ${totalAchievementsLength}`
            }
        }
    }
</script>

<style scoped lang='scss'>
    .user-progress__status {
        text-transform: uppercase;
        color: $primaryColorActive;
        font-weight: bold;
        font-size: 20px;
        line-height: 24px;
        text-align: center;
        margin-top: 10px;
    }

    .user-progress__description {
        color: $secondaryTextColor;
        margin: 15px 2vw 25px;
        text-align: center;
    }
</style>
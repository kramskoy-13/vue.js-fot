<template>
    <div class="reward__wrapper" v-show="isActiveTab">

        <Timeline />

        <div class="user-character__wrapper">
            <UserAvatar :charachterName="charachterName"
                        :userHasCharacter="userHasCharacter"
                        :charachterAvatar="charachterAvatar"
                        :openCreateUserTab="openCreateUserTab"/>

            <!--<div v-if="userHasCharacter">
                <UserHasCharacter :charachterName="charachterName" :charachterAvatar="charachterAvatar" />
            </div>

            <div v-else>
                <UserHasNoCharacter :openCreateUserTab="openCreateUserTab" />
            </div>-->
        </div>

        <UserProgress :userStatus="userStatus" :achievements="achievements"/>
        
        <AchievementsList :achievements="achievements" />

    </div>  
</template>

<script>
    import Timeline from "./Timeline.vue"
    import AchievementsList from "../Shared/AchievementsList.vue"
    import UserAvatar from "./UserAvatar.vue"
    import UserProgress from "./UserProgress.vue"

    export default {
        name: "Reward",
        components: {
            Timeline,
            AchievementsList,
            UserAvatar,
            UserProgress
        },
        props: {
            isActiveTab: Boolean,
            userHasCharacter: Boolean,
            achievements: Array,
            toggleCreateUserTab: Function,
            avatarIcons: Array,
            userStatus: String,
            charachterName: String,
            charachterAvatar: String,
        },
        mounted() {
            console.log("Reward mounted")
        },
        data() {
            return {}
        },
        methods: {
            openCreateUserTab() {
                if (this.userHasCharacter) return
                this.$emit('toggleCreateUserTab', true)
            }
        }
    }
</script>

<style scoped lang='scss'>
    .reward__wrapper {
        padding-bottom: 25px;
    }
    .user-character__wrapper {
        margin-top: 40px;
    }
</style>
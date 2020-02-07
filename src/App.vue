<template>
    <div id="app">

        <div v-if="displayPreloader" class="preloader-wr">
            <div class="lds-ring">
                <div></div>
                <div></div>
                <div></div>
                <div></div>
            </div>
        </div>

        <div class="app__wrapper">
            <CreateUserCharacter v-if="createUserTabActive"
                                 @toggleCreateUserTab="toggleCreateUserTab"
                                 @togglePreloader="togglePreloader"
                                 @handleCharacterCreation="handleCharacterCreation"
                                 :avatarIcons="avatarIcons" />

            <div v-show="!createUserTabActive">
                <NavBar :tabs="tabs"
                        :currentTab="currentTab"
                        @setCurrentTab="setCurrentTab" />

                <Reward :isActiveTab="currentTab === 'Reward'"
                        :userHasCharacter="userHasCharacter"
                        :achievements="achievements"
                        @toggleCreateUserTab="toggleCreateUserTab"
                        :userStatus="userStatus"
                        :charachterName="charachterName"
                        :charachterAvatar="charachterAvatar"
                        :avatarIcons="avatarIcons" />

                <History :isActiveTab="currentTab === 'History'" />

                <Rating :isActiveTab="currentTab === 'Rating'" />
            </div>
        </div>

    </div>
</template>

<script>
    import NavBar from "./components/NavBar.vue";
    import Reward from "./components/Reward/Reward.vue";
    import History from "./components/History/History.vue";
    import Rating from "./components/Rating/Rating.vue";
    import CreateUserCharacter from "./components/CreateUserCharacter/CreateUserCharacter.vue";
    // icons
    import icon_1 from './assets/pm_icons/icon_1.svg'
    import icon_2 from './assets/pm_icons/icon_2.svg'
    import icon_3 from './assets/pm_icons/icon_3.svg'
    import icon_4 from './assets/pm_icons/icon_4.svg'
    // mocks
    import userData from "./mocks/userdata.js"

    const tabs = [
        {
            component: "Reward",
            text: "Мої нагороди"
        },
        //{
        //    component: "Rating",
        //    text: "Рейтинг"
        //},
        //{
        //    component: "History",
        //    text: "Історія"
        //}
    ];

    const avatarIcons = [
        icon_1, icon_2, icon_3, icon_4
    ]

    export default {
        name: "app",
        components: {
            NavBar,
            Reward,
            Rating,
            History,
            CreateUserCharacter
        },
        data() {
            return {
                //tabs
                createUserTabActive: false,
                currentTab: "Reward",
                tabs: tabs,
                //preloader
                displayPreloader: false,
                // user data
                userHasCharacter: false, // should be false
                userStatus: "Новачок",               
                // character's data
                charachterName: "",
                charachterAvatar: "",
                // achievements
                achievements: [],
                //icons
                avatarIcons
            };
        },
        mounted() {
            console.log('app mounted')
            this.getUserData()
        },
        methods: {
            setCurrentTab(tab) {
                this.currentTab = tab
            },
            handleCharacterCreation(userDataObj) {
                this.userHasCharacter = true
                this.charachterName = userDataObj.charachterName
                this.charachterAvatar = userDataObj.charachterAvatar
            },
            getUserData() {
                this.userHasCharacter = userData.userHasCharacter
                this.charachterName = userData.userCharacterData.charachterName
                this.userStatus = userData.userCharacterData.userStatus
                this.charachterAvatar = userData.userCharacterData.charachterAvatar
                this.achievements = userData.achievements
            },
            toggleCreateUserTab(flag) {
                this.createUserTabActive = flag
            },
            togglePreloader() {
                this.displayPreloader = !this.displayPreloader
            }
        }
    };
</script>

<style lang="scss">

    #app {
        margin: 0;
        padding: 0;
        width: 100%;
        height: 100vh;
        display: flex;
        justify-content: center;
        padding: 5px 25px;
    }

    .app__wrapper {
        width: 100%;
        border-radius: 5px;
        max-width: 440px;
        justify-content: space-between;
    }

    .start-screen {
        position: relative;
        width: 100%;
        height: 100%;
    }
</style>

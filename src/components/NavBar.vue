<template>
    <div class="nav__wrapper">
        <div v-for="tab in tabs" class="nav__item" v-bind:class="{ active: currentTab === tab.component }" @click="$emit('setCurrentTab', tab.component)">
            {{ tab.text }}
        </div>
    </div>
</template>

<script>
    export default {
        name: "NavBar",
        props: {
            tabs: {
                type: Array
            },
            currentTab: {
                type: String
            },
            setCurrentTab: {
                type: Function
            }
        },
        data() {
            return {};
        }
    }
</script>

<style scoped lang='scss'>
    .nav__wrapper {
        display: flex;
        justify-content: space-between;
    }
    .nav__item {
        display: flex;
        align-items: center;
        text-align: center;
        line-height: 19px;
        font-style: normal;
        font-weight: bold;
        font-size: 14px;
        letter-spacing: 1px;
        text-transform: uppercase;
        color: $primaryColorNotSelected;
        padding: 10px 0;
    }
        .nav__item:hover {
            cursor: pointer;
        }
        .nav__item.active {
            color: $primaryColorActive;
        }
</style>
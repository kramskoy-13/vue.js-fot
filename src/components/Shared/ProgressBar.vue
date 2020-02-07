<template>
    <div class="progress-line__wrapper">
        <div class="progress__item" :style="{width: percantageComputed }"></div>
    </div>
</template>


<script>
    export default {
        name: "ProgressBar",
        props: {
            percantage:  Number
        },
        data() {
            return {};
        },
        computed: {
            percantageComputed() {
                return this.percantage + '%'
            },
        },
        mounted() {
            console.log('ProgressBar mounted')
        }
    }
</script>

<style scoped lang='scss'>
    .progress-line__wrapper {
        height: 2px;
        background-color: $progressBar;
        border-radius: 5px;
        margin-top: 20px;
        overflow: hidden;
    }

    .progress__item {
        height: 100%;
        background: $primaryLinearGradient;
        border-radius: 5px;
    }
</style>
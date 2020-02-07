<template>
    <div class="timeline__wrapper">
        <h4 class="timeline__header">
            {{ timelineText }}
        </h4>
        <div class="period__wrapper">
            <div class="interval__wrapper">
                <span class="interval__item"> {{ startDateComputed }}</span>
                <span> - </span>
                <span class="interval__item">{{ endDateComputed }}</span>
            </div>
            <div class="duration__wrapper">
                <span>Залишилось {{ daysLeft }} дней</span>
            </div>
        </div>
        <ProgressBar :percantage="percantage" />
    </div>
</template>

<script>
    import timeline from "../../mocks/timeline.js"
    import ProgressBar from "../Shared/ProgressBar.vue"

    const oneDay = 24 * 60 * 60 * 1000;

    export default {
        name: "Timeline",
        props: {},
        components: {
            ProgressBar
        },
        data() {
            return {
                startDate: null,
                endDate: null,
                timelineText: null
            }
        },
        mounted() {
            console.log('Timeline mounted')
            this.getTimelineData()
        },
        computed: {
            startDateComputed() {
                return this.startDate && new Date(this.startDate).toLocaleDateString().replace(/\//g, '.')
            },
            endDateComputed() {
                return this.endDate && new Date(this.endDate).toLocaleDateString().replace(/\//g, '.')
            },
            daysLeft() {
                return this.endDate && Math.round(Math.abs((this.endDate - new Date()) / oneDay));
            },
            percantage() {
                return this.startDate && this.endDate && Math.round(Math.abs((new Date() - this.startDate) / oneDay)) / Math.round(Math.abs((this.endDate - this.startDate) / oneDay)) * 100;
            },
            //width() {
            //    return {
            //        width: this.percantage + '%'
            //    }
            //}
        },
        methods: {
            getTimelineData: function () {
                this.startDate = timeline.startDate
                this.endDate = timeline.endDate
                this.timelineText = timeline.timelineText
            }
        }
    }
</script>

<style scoped lang='scss'>
    .timeline__wrapper {
        background-color: $primaryBackgroundColor;
        padding: 15px 20px;
        border-radius: 5px;
        margin-top: 15px;
    }
    .timeline__time-left {

    }
    .timeline__header {
        font-weight: 600;
        font-size: 16px;
        line-height: 24px;
    }
    .period__wrapper {
        display: flex;
        justify-content: space-between;
        margin-top: 10px;
        font-size: 10px;
        line-height: 24px;
    }
    .interval__wrapper {
        color: $primaryColorActive;
        font-weight: 600;
    }
    .duration__wrapper {
        color: $secondaryColorActive;
    }
</style>
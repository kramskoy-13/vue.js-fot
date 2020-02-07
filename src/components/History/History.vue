<template>
    <div class="history__wrapper" v-show="isActiveTab">
        History
    </div>
</template>

<script>
    export default {
        name: "History",
        props: {
            isActiveTab: {
                type: Boolean,
                default: false
            }
        },
        data() {
            return {};
        }
    }
</script>
<template>
    <div class="rating__wrapper" v-show="isActiveTab">
       Rating
    </div>
</template>

<script>
    export default {
        name: "Rating",
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
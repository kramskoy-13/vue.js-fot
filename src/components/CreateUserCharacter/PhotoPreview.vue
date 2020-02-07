<template>
    <div>
        <div class="preview__wrapper preview__wrapper_background">
            <div class="preview__text" @click="handleClick">
                <slot></slot>
            </div>
        </div>
        <div class="preview__wrapper">
            <span class="preview__text">
                Обрати інше фото
            </span>

            <img class="preview__icon" src="../../assets/selectPhotoIcon.svg" alt="select photo icon" />

            <input name="userPhoto" type="file" @change="handleChange">
        </div>
    </div>
</template>

<script>
    export default {
        name: "PhotoPreview",
        props: {
            clickHandler: Function,
            changeHandler: Function
        },
        data() {
            return {}
        },
        methods: {
            handleClick(event) {
                this.$emit('clickHandler', event)
            },
            handleChange(event) {
                this.$emit('changeHandler', event)
            }
        }
    }
</script>

<style scoped>
    .preview__wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        color: $primaryColorActive;
        padding: 10px 25px;
        border-radius: 6px;
        font-weight: normal;
        font-size: 14px;
        line-height: 18px;
    }

    .preview__wrapper_background {
        background: $primaryTextColor;
        color: white;
    }

    .preview__text {
        margin-right: 15px;
    }

    .preview__icon {
        margin-top: -10px;
    }
</style>
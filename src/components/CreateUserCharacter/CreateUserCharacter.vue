<template>
    <div class="create-character__wrapper">

        <div class="back-button__wrapper">
            <button  class="back-button__button" @click="backToMainPage">
                <img src="../../assets/backButtonArrow.svg" alt="back button" />
                <span>Назад</span>
            </button>
        </div>

        <div v-if="photoPreviewed" class="photo-wrapper">
            <img class="photo-choosen" :src="photoPreviewSRC" alt="user avatar" ref="myImg" />
        </div>

        <div v-else class="swiper-wrapper">
            <swiper :options="swiperOption" @slideChange="getSwiperIndex" ref="mySwiper">
                <swiper-slide v-if="!photoIsSaved">
                    <div class="abs-center">
                        <div class="select-photo">
                            <Icon :iconDateBase64="selectUserIcon" IMGstyle="margin-top: -7px; margin-left: 5px; width: 42px;" />
                            <input name="userPhoto" type="file" @change="previewFiles">
                        </div>
                    </div>
                </swiper-slide>
       
                <swiper-slide v-else>
                    <div class="abs-center">
                        <Icon :iconDateBase64="photoPreviewSRC" />
                    </div>
                </swiper-slide>

                <swiper-slide v-for="(iconDateBase64, index) in avatarIcons" :key="index">
                    <div class="abs-center">
                        <Icon :iconDateBase64="iconDateBase64" />
                    </div>
                </swiper-slide>
            </swiper>
            <!-- Optional controls -->
            <!-- initially pagination has been positioned inside swiper tag -->
            <div class="swiper-pagination" slot="pagination"></div>
        </div>

        <form @submit="createUserCharacter" class="create-character__form">
            <div class="form-wrapper">

                <PhotoPreview v-if="photoPreviewed" @clickHandler="saveUserPhoto" @changeHandler="previewFiles">
                    Готово
                </PhotoPreview>
               
                <PhotoPreview v-if="photoIsSaved && activeIconIndex === 0" @clickHandler="switchBackToAvataIcons" @changeHandler="previewFiles">
                    Видалити
                </PhotoPreview>

                <p class="instruction-text" v-if="!photoPreviewed">
                    Завантажуйте своє фото або обирайте одного з запропонованих персонажів
                </p>

                <div class="select-name__wrapper">
                    <input type="text" name="name" value="" placeholder="Введіть нікнейм" @input="removeNameStatusIcons" ref="myTextInput" />
                    <div v-if="nameAlreadyExistsError">
                        <img class="select-name__icon" src="../../assets/nameNotApproved.svg" alt="Name Not Approved" />
                        <p class="select-name__error-message">
                            Нажаль, даний нікнейм уже зайнятий.
                        </p>
                    </div>
                    <img v-if="nameHasBeenApproved && !nameAlreadyExistsError" class="select-name__icon" src="../../assets/nameApproved.svg" alt="Name Approved" />
                </div>

                <p class="create-character__text">
                    Оберіть персонажа та нікнейм для нього, та отримайте нагороду!
                </p>

                <input class="main-btn create-character__submit" type="submit" value="Зберегти персонажа" :disabled="nameFieldIsEmpty || (activeIconIndex === 0 && !photoPreviewSRC)" />
            </div>
        </form>   

    </div>
</template>

<script>
    import Icon from "../Shared/Icon.vue"
    import PhotoPreview from "./PhotoPreview.vue"
    import SelectUserIcon from "../../assets/selectPhotoIcon.svg"
    //swiper
    import { swiper, swiperSlide } from "vue-awesome-swiper"
    import "swiper/dist/css/swiper.css"

    export default {
        name: "CreateUserCharacter",
        components: { Icon, PhotoPreview, swiper, swiperSlide },
        props: {
            toggleCreateUserTab: Function,
            togglePreloader: Function,
            handleCharacterCreation: Function,
            avatarIcons: Array
        },
        data() {
            return {
                swiperOption: {
                    slidesPerView: 3,
                    spaceBetween: 60,
                    centeredSlides: true,
                    //loop: true,
                    pagination: {
                        el: '.swiper-pagination',
                        clickable: true
                    }
                },
                nameFieldIsEmpty: true,
                photoPreviewed: false,
                photoPreviewSRC: "",
                photoIsSaved: false,
                activeIconIndex: 0,
                nameAlreadyExistsError: false,
                nameHasBeenApproved: false,
                selectUserIcon: SelectUserIcon,
                //delete
                customFlag: true
            }
        },
        methods: {
            backToMainPage() {
                this.$emit('toggleCreateUserTab', false)
            },
            removeNameStatusIcons(event) {
                this.nameAlreadyExistsError = false
                this.nameHasBeenApproved = false
                this.nameFieldIsEmpty = event.target.value.length === 0
            },
            getSwiperIndex() {
                this.activeIconIndex = this.$refs.mySwiper.swiper.realIndex
            },
            switchBackToAvataIcons() {
                this.photoPreviewed = false
                this.photoPreviewSRC = "" 
                this.photoIsSaved = false
                this.$refs.mySwiper.swiper.updateSlides()
            },
            saveUserPhoto() {
                this.photoIsSaved = true
                this.photoPreviewed = false
            },
            previewFiles(event) {
                const { target } = event
                if (!target || !target.files || !target.files[0]) return 

                this.photoIsSaved = false

                const self = this
                const reader = new FileReader()

                self.photoPreviewed = true

                reader.onload = function (e) {
                    self.photoPreviewSRC = e.target.result

                }
                reader.readAsDataURL(target.files[0])
            },
            createUserCharacter(event) {
                event.preventDefault()
                
                const textInput = this.$refs.myTextInput
                 // trim white space
                textInput.value = textInput.value.trim()

                if (textInput.value.length === 0) {
                    this.nameFieldIsEmpty = true
                    return 
                }

                this.$emit('togglePreloader')

                setTimeout(() => {
                    this.$emit('togglePreloader')
                    if (this.customFlag) {
                        //error occured
                        this.nameAlreadyExistsError = true
                    }
                    else {
                        // validation passed
                        this.nameAlreadyExistsError = false
                        this.nameHasBeenApproved = true
                        // object with user data which is sent to server
                        const userData = {
                            charachterName: textInput.value,
                            charachterAvatar: this.photoPreviewSRC ? this.photoPreviewSRC : this.avatarIcons[this.activeIconIndex - 1] // -1 is needed due to the first slider at 0 position is select user photo
                        }
   
                        setTimeout(() => {
                            this.$emit('handleCharacterCreation', userData)
                            this.backToMainPage()
                        }, 1000)
                    }
                    //delete
                    this.customFlag = !this.customFlag
                }, 500)
            }
        }

    }
</script>

<style scoped>
    input[type="text"] {
        border: none;
        border-bottom: 1px solid $primaryColorNotSelected;
        font-weight: bold;
        font-size: 20px;
        line-height: 24px;
        color: $primaryColorActive;
        text-align: center;
        padding: 10px 15px;
        width: 75%;
    }
    input[type="submit"]:disabled {
        background: $primaryColorNotSelected;
    }
    ::-webkit-input-placeholder { /* Chrome/Opera/Safari */
        color: $primaryColorNotSelected;
    }

    ::-moz-placeholder { /* Firefox 19+ */
        color: $primaryColorNotSelected;
    }

    :-ms-input-placeholder { /* IE 10+ */
        color: $primaryColorNotSelected;
    }

    :-moz-placeholder { /* Firefox 18- */
        color: $primaryColorNotSelected;
    }
    .instruction-text {
        font-style: normal;
        font-weight: normal;
        font-size: 14px;
        line-height: 18px;
        text-align: center;
        color: $secondaryColorActive;
        padding: 15px 35px;
    }
    .form-wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 15px;
    }

    .back-button__button {
        color: $primaryColorActive;
        font-weight: normal;
        font-size: 14px;
        line-height: 19px;
        background: none;
        border: none;
    }

    .back-button__wrapper {
        margin: 15px 0;
        align-self: flex-start;
    }

    .photo-wrapper {
        height: 200px;
        display: flex;
        justify-content: center;
        align-items: center;

        width: 200px;
        border-radius: 50%;
        overflow: hidden;
    }

    .photo-choosen {
        /*height: auto;*/
        max-height: 200px;
        display: block;
        /*max-width: 100%;*/
    }

    .select-name__wrapper {
        position: relative;
        text-align: center;
    }

    .select-name__icon {
        position: absolute;
        top: 20px;
        right: 36px;
    }

    .select-name__error-message {
        font-style: normal;
        font-weight: normal;
        font-size: 12px;
        line-height: 20px;
        text-align: center;
        color: $errorMessageColor;
        margin-top: 10px;
    }

    .create-character__wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        overflow: hidden;
    }

    .swiper-wrapper {
        width: 141%;
        height: 250px;
    }

    .swiper-container {
        height: 200px;
    }

    .swiper-slide {
        text-align: center;
        /*margin: 0 auto;*/
        width: 200px;
        /*min-width: 200px;*/
        transform: scale(.65);
        opacity: .6;
        transition: .53s;
        position: relative;
    }

    .swiper-slide-active {
        transform: scale(1);
        opacity: 1;
    }

    .create-character__text {
        font-weight: normal;
        font-size: 14px;
        line-height: 20px;
        text-align: center;
        color: $secondaryTextColor;
        margin-top: 30px;
        padding: 0 20px;
    }

    .create-character__submit {
        margin-top: 25px;
    }

    .swiper-pagination.swiper-pagination-clickable.swiper-pagination-bullets {
        width: 200px;
        left: 50%;
        transform: translateX(-50%);
        bottom: 10px;
        display: flex;
        align-items: center;
        justify-content: space-evenly;
    }
</style>
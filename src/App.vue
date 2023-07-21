<script setup>
import {ref,reactive} from "vue"
const images = reactive([
    {
        photo: "uploads/big-1.jpg",
        thumb: "uploads/small-1.jpg"
    },
    {
        photo: "uploads/big-2.jpg",
        thumb: "uploads/small-2.jpg"
    },
    {
        photo: "uploads/big-3.jpg",
        thumb: "uploads/small-3.jpg"
    },
    {
        photo: "uploads/big-4.jpg",
        thumb: "uploads/small-4.jpg"
    }
])

const i = ref(0)
const currentPhoto = ref(images[0].photo)

const nextArrowStyle = ref('original')
const nextCursor = ref('cur_pointer')

const prevArrowStyle = ref('gray')
const prevCursor = ref('cur_none')

function nextButton() {
    prevArrowStyle.value = 'original'
    prevCursor.value = 'cur_pointer'
    if(i.value !== images.length-1) {
        i.value = i.value+1
    }
    if(i.value === images.length-1) {
        nextArrowStyle.value = 'gray'
        nextCursor.value = 'cur_none'
    }
    currentPhoto.value = images[i.value].photo
}
function prevButton() {
    nextArrowStyle.value = 'original'
    nextCursor.value = 'cur_pointer'
    if(i.value > 0) {
        i.value = i.value-1
    }
    if(i.value === 0) {
        prevArrowStyle.value = 'gray'
        prevCursor.value = 'cur_none'
    }
    currentPhoto.value = images[i.value].photo
}

function thumbClick(index) {
    currentPhoto.value = images[index].photo
    i.value = index
    if(index == 0) {
        nextArrowStyle.value = 'original'
        nextCursor.value = 'cur_pointer'
        prevArrowStyle.value = 'gray'
        prevCursor.value = 'cur_none'
    }
    else if(index == images.length-1) {
        nextArrowStyle.value = 'gray'
        nextCursor.value = 'cur_none'
        prevArrowStyle.value = 'original'
        prevCursor.value = 'cur_pointer'
    }
    else {
        nextArrowStyle.value = 'original'
        nextCursor.value = 'cur_pointer'
        prevArrowStyle.value = 'original'
        prevCursor.value = 'cur_pointer'
    }
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12">
                <h2>Image Carousel with Vue.js 3</h2>
                <div class="main d-flex justify-content-center align-items-center">
                    <div @click="prevButton()" class="left-arrow" :class="[prevArrowStyle,prevCursor]">
                        <i class="fa-solid fa-circle-arrow-left"></i>
                    </div>
                    <div class="main-photo">
                        <div class="item"><img :src="currentPhoto" alt=""></div>
                        <div class="small-photos">
                            <div class="small-photo" v-for="(image,index) in images" :key="index">
                                <img @click="thumbClick(index)" :src="image.thumb" alt="">
                            </div>
                        </div>
                    </div>
                    <div @click="nextButton()" class="right-arrow" :class="[nextArrowStyle,nextCursor]">
                        <i class="fa-solid fa-circle-arrow-right"></i>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
</style>
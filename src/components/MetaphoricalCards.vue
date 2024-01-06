<script setup>
import { ref, watch } from 'vue';

const formShow = ref(false);
const cardСategory = ref("");

const toggleForm = () => {
    formShow.value = !formShow.value;
    document.body.style.overflow = formShow.value ? 'hidden' : '';
    cardСategory.value = "";
};



// Генерация карточек
const cardNumber = ref("");
const allСardNumber = ref(0);
const randomOrder = ref([]);
const sequentialOrder = ref([]);

watch(cardСategory, () => {
    if (cardСategory.value === 'source'){
        allСardNumber.value = 80;
    }else if(cardСategory.value === 'money'){
        allСardNumber.value = 50;
    }

    randomOrder.value = Array.from({ length: allСardNumber.value }, (_, index) => index + 1)
    .sort(() => Math.random() - 0.5);

    sequentialOrder.value = Array.from({ length: allСardNumber.value }, (_, index) => index + 1);
});

const toggleBefore = (event) => {
    const cardItem = event.target.closest('.card__item');
    const cardItemHiden = event.target.closest('.card__hide');
    const fullscreen = document.querySelector('.fullscreen');
    if (cardItemHiden){
        cardItemHiden.classList.add('hide-before');
    }

    if (cardItem) {
        cardItem.addEventListener('click', () => {
            const imageSrc = cardItem.querySelector('img').getAttribute('src');
            fullscreen.querySelector('img').setAttribute('src', imageSrc);
            fullscreen.classList.toggle('show');
        });
    }
};

const CloseFullscreen = () =>{
    const fullscreen = document.querySelector('.fullscreen');
    fullscreen.classList.remove('show');
}
</script>


<template>
    <div @click="toggleForm" class="card__button">
        <img src="../assets/img/cards.png" alt="">
    </div>

    <div v-if="formShow" class="overlay">
        <div class="form">
            <div v-if="cardСategory" class="search__container">
                <p class="countCard">Всего карт: {{ allСardNumber }}</p>
                <i class="bi bi-search card__search_icon"></i>
                <input v-model="cardNumber" type="text" class="card__search" placeholder="Поиск по номеру карты">
            </div>

            <div @click="toggleForm" class="cross-icon"></div>
            <div class="cross-icon-silver"></div>
            <div class="cross-icon-silver-second"></div>
            
            <div v-if="!cardСategory" class="cards__list">
                <div class="cards__category">
                    <h3 class="category__title">Выберите категорию карты:</h3>
                    <div class="category__list">
                        <div @click="cardСategory='money'" class="category__item">
                            Денежные
                        </div>
                        <div @click="cardСategory='source'" class="category__item">
                            Ресурсные
                        </div>
                    </div>
                </div>
            </div>
                

            <!-- Генерация самих карточек -->
            <div class="cards__list" v-if="cardСategory">
                <div v-if="!cardNumber" v-for="(i, index) in sequentialOrder" class="card__item" @click="toggleBefore">
                    <img :src="`/src/assets/img/cards/${cardСategory}/card${randomOrder[index]}.jpg`" alt="">
                    <div class="card__hide">{{ i }}</div>
                </div>
                <div v-if="cardNumber" v-for="(i, index) in sequentialOrder">
                    <div v-if="cardNumber == i"  class="card__item" @click="toggleBefore">
                        <img :src="`/src/assets/img/cards/${cardСategory}/card${randomOrder[index]}.jpg`" alt="">
                        <div class="card__hide">{{ i }}</div>
                    </div>
                </div>
                <div v-else-if="cardNumber && (cardNumber < 1 || cardNumber > allСardNumber)" class="card__item" @click="toggleBefore">
                    <h2>Такой карточки нет</h2>
                </div>
            
                <!-- Открытие картинки на всю страницу -->
                <div class="fullscreen" @click="CloseFullscreen()">
                    <img src="" alt="" class="fullscreen__img">
                </div>
            </div>

        </div>
    </div>
</template>

<style scoped>
    .countCard{
        margin-right: 30px;
    }
    .fullscreen{
        display: none;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.7);
        z-index: 11;
        -webkit-backdrop-filter: saturate(180%) blur(10px);
        backdrop-filter: saturate(180%) blur(10px);
        padding: 30px;
    }
    .fullscreen.show{
        display: block;
    }
    .card__item{
        position: relative;
        width: 200px;
        height: 277px;
        border-radius: 5px;
        overflow: hidden;
        border: 1px solid #353535;
        flex-grow: 0;
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .card__hide{
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        background-color: rgba(255, 245, 196, 0.6);
        backdrop-filter: blur(30px);
        width: 100%;
        height: 100%;
        z-index: 1;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 40px;
        font-weight: 900;
        color: rgb(112, 112, 112);
    }
    .hide-before{
        display: none;
    }
    .card__item img{
        object-fit: cover;
    }
    .category__title{
        width: 100%;
        text-align: center;
    }
    .category__item{
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: aliceblue;
        padding: 30px;
        border-radius: 10px;
        cursor: pointer;
        width: 100%;
        height: 100%;
        font-size: 30px;
    }
    .cards__category{
        width: 90%;
        height: 90%;
    }
    .category__list{
        margin-top: 20px;
        display: flex;
        gap: 20px;
        width: 100%;
        height: 100%;
    }
    .search__container{
        width: 100%;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }
    .card__search{
        position: relative;
        border-radius: 10px;
        stroke: none;
        border: 1px solid rgb(255, 207, 145);
        padding: 5px 5px 5px 30px;
        font-size: 20px;
        width: 300px;
    }
    .card__search_icon{
        margin-right: -25px;
        z-index: 2;
    }
    .cards__list{
        background-color: #fff;
        margin-top: 10px;
        padding: 30px;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 10px;
        flex-wrap: wrap;
        overflow-y: auto;
        margin-right: 0;
        height: 80vh;
        min-width: 80vw;
    }
    .form{
        background-color: antiquewhite;
        padding: 30px;
        border-radius: 15px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        z-index: 12;
    }
    .card__button{
        position: fixed;
        right: 30px;
        bottom: 95px;
        width: 50px;
        height: 50px;
        border-radius: 10px;
        background-color: white;
        box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
        -webkit-box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
        -moz-box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
        z-index: 10;
        cursor: pointer;
        padding: 5px;
    }
    .card__button:hover{
        border: 1px solid #353535;
        box-shadow: none;
        -webkit-box-shadow: none;
        -moz-box-shadow: none;
    }
    .cross-icon, .cross-icon-silver-second, .cross-icon-silver {
        position: absolute;
        background-color: rgb(254, 55, 55);
        top: 15px;
        left: 15px;
        width: 15px;
        height: 15px;
        cursor: pointer;
        border-radius: 50%;
    }
    .cross-icon-silver, .cross-icon-silver-second{
        background-color: #353535;
        left: 35px;
        cursor: default;
    }
    .cross-icon-silver-second{
        left: 55px;
    }
    .overlay{
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.7);
        z-index: 11;
        -webkit-backdrop-filter: saturate(180%) blur(10px);
        backdrop-filter: saturate(180%) blur(10px);
    }
</style>
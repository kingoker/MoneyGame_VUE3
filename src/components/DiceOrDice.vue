<script setup>
    import { ref } from 'vue';
    import DiceBox from "@3d-dice/dice-box";

    const formShow = ref(false);

    const toggleForm = () => {
        formShow.value = !formShow.value;
        if (formShow.value) {
            document.body.style.overflow = 'hidden';
        } else {
            document.body.style.overflow = '';
        }
    };

    // Бросок кубика
    const rollCube = (type) => {
        const diceFloor = document.getElementById('dice-floor');

        // Удаляем все дочерние элементы (все canvas)
        while (diceFloor.firstChild) {
            diceFloor.firstChild.remove();
        }

        let Box = new DiceBox("#dice-floor", {
            assetPath: "/public/assets/dice-box/",
            scale: 13,
            offscreen: true,
            width: '100%',
            height: '100%',
        });

        Box.init().then(async () => {
            Box.roll([`1d${type}`]);
        });
    }
</script>

<template>
    <!-- Кнопка -->
    <div @click="toggleForm" class="dice__button">
        <img src="../assets/img/cubic.png" alt="">
    </div>

    <!-- Поле кубиков -->
    <div v-if="formShow" class="overlay">
        <div class="form">
            <div @click="toggleForm" class="cross-icon"></div>
            <div class="cross-icon-silver"></div>
            <div class="cross-icon-silver-second"></div>

            <div class="dice__floor cube_wrapper" id="dice-floor">

            </div>

            <div class="cube__buttons">
                <button class="dice__start" @click="rollCube(6)">Бросить 6</button>
                <button class="dice__start" @click="rollCube(10)">Бросить 10</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.dice__floor{
    width: 600px;
    height: 300px;
    background-color: #fff;
    border-radius: 7px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    perspective: 400px;
    box-sizing: border-box;
    margin-top: 20px;
}
.dice__start{
    stroke: none;
    border: none;
    width: 100%;
    background-color: chocolate;
    color: #fff;
    height: 50px;
    margin-top: 10px;
    border-radius: 10px;
    font-size: 24px;
    cursor: pointer;
}
.dice__start:hover{
    background-color: rgb(171, 84, 21);
}
    .cube__buttons{
        display: flex;
        gap: 10px;
    }
    .dice__button{
        position: fixed;
        right: 30px;
        bottom: 30px;
        width: 50px;
        height: 50px;
        border-radius: 10px;
        background-color: white;
        box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
        -webkit-box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
        -moz-box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
        z-index: 10;
        cursor: pointer;
    }
    .dice__button:hover{
        border: 1px solid #353535;
        box-shadow: none;
        -webkit-box-shadow: none;
        -moz-box-shadow: none;
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
</style>
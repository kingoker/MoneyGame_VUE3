<script setup>

</script>


<template>
    <header class="header">
        <div class="header__container container">
            <a class="header__logo" href="/">
                <img src="../assets/img/logo.webp" alt="Денежная Акация">
                <p class="header__logo_text">Денежная<br>Акация</p>
            </a>
            
            <div class="header__list">
                <a href="" class="header__item">Карта</a>
                <a href="" class="header__item">Карточки</a>
            </div>
            <div></div>
        </div>
    </header>
</template>


<style scoped>
    .header__list{
        display: flex;
        gap: 15px;
    }
    .header__item{
        text-decoration: none;
        font-weight: 700;
        color: green;
    }
    .header__item:hover{
        color: rgb(0, 99, 0);
    }
    .header{
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        z-index: 10;
        display: flex;
        align-items: center;
        background-color: #fff;
        height: 50px;
        box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
        -webkit-box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
        -moz-box-shadow: 0px 0px 10px 5px rgba(122,122,122,0.76);
    }
    .header__container{
        display: flex;
        justify-content: space-between;
        width: 100%;
    }
    .header__logo{
        display: flex;
        align-items: center;
        gap: 5px;
        width: 30px;
        height: 30px;
        text-decoration: none;
    }
    .header__logo_text{
        font-size: 14px;
        font-weight: 700;
        line-height: 14px;
        color: green;
    }
</style>
<template>
    <ul class="navbar">
        <li class="main">
            <div class="icon"> <img src="@/assets/img/main-page.svg" alt="Главная"> </div>
            <span class="label">Главная</span>
        </li>

        <li class="orders">
            <div class="icon"> <img src="@/assets/img/orders.svg" alt="Сделки"> </div> 
            <span class="label">Сделки</span>
        </li>

        <li class="objects">
            <div class="icon"> <img src="@/assets/img/objects.svg" alt="Объекты"> </div>
            <span class="active-label">Объекты</span>
        </li>

        <li class="card">
            <div class="icon"> <img src="@/assets/img/card.svg" alt="Визитка"> </div> 
            <span class="label">Визитка</span>
        </li>

        <li class="profile">
            <div class="icon"> <img src="@/assets/img/avatar.svg" alt="Профиль"> </div>
            <span class="label">Профиль</span>
        </li>
    </ul>
</template>

<script>
    export default {
        name: 'MobileNavbar'
    };
</script>

<style scoped>
    .navbar {
        display: flex;
        flex-direction: column;
        list-style-type: none;
        box-shadow: 0px 0px 8px 0px #1E1E241A;
        user-select: none;
    }

    @media (min-width: 320px) and (max-width: 1365px) {
        .navbar {
            flex-direction: row;
            position: fixed;
            bottom: 0;
            width: 100%;
            background-color: #FFFFFF;
            z-index: 1;
            padding-top: 4px;
        }
        
        .main,
        .orders,
        .objects,
        .card,
        .profile {
            width: 20%;
        }

        .label {
            font-weight: 500;
            font-size: 10px;
            line-height: 12px;
            text-align: center;
            color: #9596A7;
        }

        .active-label {
            font-weight: 500;
            font-size: 10px;
            line-height: 12px;
            text-align: center;
            color: #6F77FE;
        }

        .icon {
            width: 28px;
            height: 28px;
            margin: auto;
        }

        .icon img {
            display: flex;
            align-items: center;
            vertical-align: middle;
            justify-content: center;
            width: 100%;
        }
    }

    @media (min-width: 1366px) {
        .navbar {
            flex-direction: column;
            position: fixed;
            top: 0;
            left: 0;
            background-color: #FFFFFF;
            z-index: 1;
            width: 80px;
            height: 100%;
        }
    }
</style>
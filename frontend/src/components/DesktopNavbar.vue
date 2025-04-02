<template>
    <ul class="navbar 1">
        <div class="navbar-section">
            <li class="logo-navbar">
                <a class="logo" href="#">
                    <img src="@/assets/img/logo-navbar.svg" width="42px" height="42px" alt="Логотип компании">
                </a>
            </li>

            <li class="main">
                <a href="#" class="main-href">
                    <div class="icon"> <img src="@/assets/img/main-page.svg" alt="Главная"> </div>
                    <span class="label">Главная</span>
                </a>
            </li>

            <li class="orders">
                <a href="#" class="orders-href">
                    <div class="icon"> <img src="@/assets/img/orders.svg" alt="Сделки"> </div> 
                    <span class="label">Сделки</span>
                </a>
            </li>

            <li class="objects">
                <a href="#" class="objects-href">
                    <div class="icon"> <img src="@/assets/img/objects.svg" alt="Объекты"> </div>
                    <span class="active-label">Объекты</span>
                </a>
            </li>

            <li class="control">
                <a href="#" class="control-href">
                    <div class="icon"> <img src="@/assets/img/control-logo-navbar.svg" alt="Управление"> </div>
                    <span class="active-label">Управление</span>
                </a>
            </li>

            <li class="developer">
                <a href="#" class="developer-href">
                    <div class="icon"> <img src="@/assets/img/developer-logo-navbar.svg" alt="Разработчик"> </div>
                    <span class="active-label">Разработчик</span>
                </a>
            </li>
        </div>
        <div class="navbar-section">
            <li class="card">
                <a href="#" class="card-href">
                    <div class="icon"> <img src="@/assets/img/card.svg" alt="Визитка"> </div> 
                    <span class="label">Визитка</span>
                </a>
            </li>

            <li class="profile">
                <a href="#" class="profile-href">
                    <div class="icon"> <img src="@/assets/img/avatar.svg" alt="Профиль"> </div>
                    <span class="label">Профиль</span>
                </a>
            </li>
        </div>
    </ul>
</template>

<script>
    export default {
        name: 'DesktopNavbar'
    };
</script>

<style scoped>
    .navbar {
        display: flex;
        flex-direction: column;
        list-style-type: none;
        user-select: none;
        flex-direction: column;
        position: fixed;
        top: 0;
        left: 0;
        background-color: #FFFFFF;
        z-index: 10;
        width: 80px;
        height: 100%;
        justify-content: space-between;
        border-right: 1px solid #DDDDE3;
    }

    .navbar-section {
        display: flex;
        flex-direction: column;
        gap: 11px;
    }

    .navbar-section li {
        width: 80px;
        height: 64px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    
    .navbar-section a {
        text-decoration: none;
        font-weight: 500;
        font-size: 10px;
        line-height: 12px;
        text-align: center;
        color: #9596A7;
    }
</style>
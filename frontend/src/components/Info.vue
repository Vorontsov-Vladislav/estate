<template>
    <div class="info">
        <div class="info-subtitle">
            Найдено объектов: 25
        </div>

        <div class="info-filters">
            <div class="filter-item"> 
                <span class="filter-text">Краснодар</span> 
                <button class="filter-remove-btn">
                    <img src="@/assets/img/remove-filter-btn.svg" alt="Удалить">
                </button>
            </div>

            <div class="filter-item"> 
                <span class="filter-text">ЖК «ITRIELT»</span> 
                <button class="filter-remove-btn">
                    <img src="@/assets/img/remove-filter-btn.svg" alt="Удалить">
                </button>
            </div>

            <div class="filter-item"> 
                <span class="filter-text">Литер 1</span> 
                <button class="filter-remove-btn">
                    <img src="@/assets/img/remove-filter-btn.svg" alt="Удалить">
                </button>
            </div>

            <div class="filter-item"> 
                <span class="filter-text">Этаж 2</span> 
                <button class="filter-remove-btn">
                    <img src="@/assets/img/remove-filter-btn.svg" alt="Удалить">
                </button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Info'
    };
</script>

<style scoped>
    .info {
        padding: 8px;
        border-bottom: 1px solid #ECEDF0;
        display: flex;
        flex-direction: column;
        row-gap: 8px;
    }

    .info-subtitle {
        font-weight: 600;
        font-size: 20px;
        line-height: 24px;
        color: #1E1E24;
        height: 24px;
        text-align: left;
        user-select: none;
    }

    .info-filters {
        display: flex;
        flex-wrap: wrap;
        flex-direction: row;
        gap: 4px;
    }

    .filter-item {
        height: 28px;
        border-radius: 6px;
        border: 1px solid #DDDDE3;
        background-color: #FFFFFF;
        padding: 6px 6px 6px 8px;
        display: flex;
        gap: 4px;
        align-items: center;
    }

    .filter-remove-btn {
        width: 16px;
        height: 16px;
        border: 0px;
        background-color: transparent;
        padding: 0px;
        display: flex;
        align-items: center;
        justify-content: center;
        user-select: none;
    }

    .filter-remove-btn:hover {
        cursor: pointer;
    }

    .filter-text {
        user-select: none;
    }

    @media (min-width: 744px) {
        .info {
            padding: 16px;
        }

    }

</style>
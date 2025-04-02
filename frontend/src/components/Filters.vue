<template>
    <div class="filters">
        <span class="filter-icon"><img src="@/assets/img/filter.svg" alt=""></span>

        <div class="filter-title" v-if="typeDevice !== 'Mobile'">
            Фильтры
        </div>

        <div class="filter-count">
            <span class="filter-count-value">4</span>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Filters',
    data() {
        return {
            typeDevice: '',
        };
    },
    methods: {
        checkDeviceType() {
            if (window.innerWidth <= 743) {
                this.typeDevice = 'Mobile';  
            } 
            
            if (window.innerWidth >= 744 && window.innerWidth < 1366) {
                this.typeDevice = 'Tablet';
            }

            if (window.innerWidth >= 1366 && window.innerWidth < 1920) {
                this.typeDevice = 'Laptop';
            }

            if (window.innerWidth >= 1920) {
                this.typeDevice = 'Desktop';
            }
        },
    },
    mounted() {
        this.checkDeviceType();
        window.addEventListener('resize', this.checkDeviceType);
    },
    beforeDestroy() {
        window.removeEventListener('resize', this.checkDeviceType);
    },
}

</script>

<style scoped>
.filters {
    height: 36px;
    border-radius: 8px;
    display: flex;
    flex-direction: row;
    align-items: center;
    background-color: #F4F4F6;
    padding: 0px 12px;
    user-select: none;
    cursor: pointer;
}


@media (max-width: 743px) {
    .filters {
        width: 66px;
        gap: 8px;
    }
}

@media (min-width: 744px) {
    .filters {
        width: 140px;
        gap: 2px;
        margin-left: 4px;
    }

    .filter-icon {
        width: 20px;
        height: 20px;
    }

    .filter-title {
        height: 20px;
        width: 72px;
        padding: 1px 4px;
    }
}


.filter-title {
    color: #6F77FE;
}

.filter-count {
    min-width: 20px;
    min-height: 20px;
    border-radius: 50%;
    background-color: #6F77FE;
    color: #FFFFFF;
    align-items: center;
    display: flex;
    justify-content: center;
    line-height: 19px;
}

.filter-icon {
    display: flex;
    align-items: center;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>
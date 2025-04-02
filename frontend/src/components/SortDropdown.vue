<template>
    <div class="sort-dropdown">
        <button class="sort-button" :class="[isDesktopToggleOpen?'sort-button__active':'']" @click="toggleDropdown">
        <span class="icon"><img src="@/assets/img/sort.svg" alt="sort"></span>
        <div class="sort-text">
            {{ selectedSort }}
        </div>
        <span class="arrow"><img src="@/assets/img/arrow_down.svg" alt=""></span>
        </button>
        <div v-if="isDesktopToggleOpen" class="sort-dropdown-menu">
            <label v-for="option in sortOptions" :key="option.value" class="dropdown-item">
                <input 
                    type="radio" 
                    v-model="selectedSort" 
                    :value="option" 
                    class="sort-radio"
                />
                <span class="sort-dropdown-label"> {{ option }} </span>
            </label>
        </div>

        <div v-if="isMobileToggleOpen" class="modal-overlay"  @click.self="closeModal">
            <div class="modal-content">
                <label v-for="option in sortOptions" :key="option.value" class="dropdown-item">
                    <input 
                        type="radio" 
                        v-model="selectedSort" 
                        :value="option" 
                        class="sort-radio"
                    />
                    <span class="sort-dropdown-label"> {{ option }} </span>
                </label>
            </div>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            name: 'SortDropdown',
            isDesktopToggleOpen: false,
            isMobileToggleOpen: false,
            selectedSort: "Сначала с большей площадью",
            sortOptions: ["Сначала дешевле", "Сначала дороже", "Сначала с большей площадью", "Сначала с меньшей площадью"]
        };
    },
    methods: {
        toggleDropdown() {
            if (window.innerWidth <= 743) {
                this.isMobileToggleOpen = !this.isMobileToggleOpen;
            } else {
                this.isDesktopToggleOpen = !this.isDesktopToggleOpen;
            }
        },

        closeModal() {
            this.isMobileToggleOpen = false;
        },
    }
};
</script>

<style scoped>
.sort-dropdown {
    position: relative;
    display: inline-block;
    width: 220px;
    user-select: none;
}

.sort-button {
    width: 256px;
    height: 36px;
    padding: 8px 12px;
    border-radius: 8px;
    border: 0.5px solid #DDDDE3;
    color: #1E1E24;
    background: #F4F4F6;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.sort-button:hover {
    background-color: #ECEDF0;
    cursor: pointer;
}

.sort-button__active {
    background-color: #fff;
}

.sort-button__active .arrow {
    transform: rotate(180deg);
}

.icon {
    color: #6c4ae0;
}

.arrow {
    display: flex;
}

.sort-dropdown-menu {
    position: absolute;
    top: 100%;
    left: 8px;
    width: 256px;
    background-color: #FFFFFF;
    box-shadow: 0px 8px 16px 0px #17171C0D;
    border-radius: 8px;
    padding: 4px 0;
    margin-top: 8px;
    z-index: 10;
    gap: 0px;
    user-select: none;
}

.sort-dropdown-label {
    width: 200px;
    text-align: left;
}

.dropdown-item {
    display: flex;
    align-items: center;
    padding: 10px;
    cursor: pointer;
    column-gap: 8px;
}

.hidden-radio {
    display: none;
}

.sort-radio {
    margin: 0px;
    width: 20px;
    height: 20px;
    accent-color: #6F77FE;
}

.custom-radio {
    width: 16px;
    height: 16px;
    border-radius: 50%;
    border: 2px solid #B7B8C3;
    margin-right: 8px;
    display: inline-block;
}

.custom-radio.selected {
    border-color: #6c4ae0;
    background: #6c4ae0;
}

.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #9C9C9E;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    z-index: 1000;
}

.modal-content {
    background-color: #FFFFFF;
    width: 304px;
    height: 168px;
    padding: 4px 0;
    border-radius: 12px;
    border: 1px solid #ECEDF0;
    box-shadow: 0px 8px 16px 0px #17171C0D;
    font-weight: 400;
    font-size: 16px;
    line-height: 20px;
    margin-bottom: 8px;
}

@media (max-width: 743px) {
    .sort-button {
        display: flex;
        gap: 4px;
        width: 100%;
    }

    .sort-dropdown {
        display: flex;
        width: 100%;
        height: 48px;
        flex-direction: row;
        align-items: center;
    }

    .dropdown-item {
        height: 40px;
    }

    .sort-dropdown-label {
        width: 100%;
    }
}

@media (min-width: 744px) {
    .sort-button {
        margin: auto;
    }

    .sort-dropdown {
        width: 272px;
    }
}

</style>
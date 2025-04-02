<template>
    <div class="header">
      <div class="header-container" v-if="typeDevice === 'Mobile' && !isMultyActive">
        <div class="inner-header-container">
          <div class="title">
            Каталог объектов
          </div>
          <Filters></Filters>
        </div>

        <SortDropdown></SortDropdown>
      </div>

      <div class="header-container" v-if="typeDevice !== 'Mobile' && !isMultyActive">
        <div class="title">
          Каталог объектов
        </div>
        <div class="functions-group">
          <SortDropdown></SortDropdown>
          <Filters></Filters>
        </div>
      </div>

      <div class="header-container chosen" v-if="isMultyActive">
        <div class="title">
          Выбрано {{ chosenItemsCount }}
        </div>
        <div class="actions">
          <div class="add-favorite">
            <div class="icon">
              <img src="@/assets/img/favorite.svg" alt="Добавить в избранное">
            </div>
            <div class="favorite-subtitle" v-if="!blocksWithoutText">
              Добавить в избранное
            </div>
          </div>
          <div class="add-selection">
            <div class="icon">
              <img src="@/assets/img/header-selection.svg" alt="Добавить в подборку">
            </div>
            <div class="selection-subtitle" v-if="!blocksWithoutText">
              Добавить в подборку
            </div>
          </div>
          <div class="share">
            <div class="icon">
              <img src="@/assets/img/share.svg" alt="Поделиться">
            </div>
            <div class="share-subtitle" v-if="!blocksWithoutText">
              Поделиться
            </div>
          </div>
          <div class="cancel-choose" @click="cancelChoose">
            <div class="icon">
              <img src="@/assets/img/cancel-choose.svg" alt="Отменить">
            </div>
            <div class="cancel-subtitle" v-if="!blocksWithoutText">
              Отменить
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>

import SortDropdown from './SortDropdown.vue'
import Filters from './Filters.vue'

export default {
  name: 'Header',
  props: {
    isMultyActive: Boolean,
    chosenItemsCount: Number
  },
  components: {
    SortDropdown,
    Filters
  },
  data() {
    return {
      typeDevice: '',
      blocksWithoutText: true,
    };
  },
  methods: {
    checkDeviceType() {
      console.log(1)
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

      if (window.innerWidth <= 1272) {
        this.blocksWithoutText = true;
      } else {
        this.blocksWithoutText = false;
      }
    },

    cancelChoose() {
      this.$emit('cancelMultyChoose');
    }
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
.title {
  font-weight: 600;
  font-size: 17px;
  line-height: 22px;
  user-select: none;
}

.header  {
  border-bottom: 1px solid #DDDDE3;
  position: fixed;
  top: 0;
  width: calc(100% - 80px);
  background: #fff;
  z-index: 2;
}

@media (max-width: 1365px) {
  .header {
    width: 100%;
  }
}

@media (max-width: 743px) {
  .header-container {
    width: 100%;
    padding: 0 16px;
  }

  .inner-header-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 46px;
  }

  .header {
    display: flex;
    justify-content: center;
  }

  .add-favorite {
    width: 36px;
    height: 36px;
    border-radius: 8px;
    padding: 8px;
  }
}

@media (min-width: 744px) {
  .header {
    padding: 14px 16px;
    height: 64px;
  }

  .header-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }

  .functions-group {
    display: flex;
    flex-direction: row;
    gap: 4px;
  }
}

@media (max-width: 1272px) {
  .chosen {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }

  .actions {
    display: flex;
    flex-direction: row;
    gap: 8px;
    align-items: center;
    justify-content: center;
  }

  .add-favorite,
  .add-selection,
  .share,
  .cancel-choose {
    display: flex;
    flex-direction: row;
    width: 36px;
    height: 36px;
    padding: 8px;
    border-radius: 8px;
    gap: 2px;
    background-color: #F4F4F6;
    cursor: pointer;
    justify-content: center;
  }

  .cancel-choose {
    background-color: transparent;
  }

  .icon {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}

@media (min-width: 1273px) {
  .add-favorite,
  .add-selection,
  .share,
  .cancel-choose {
    display: flex;
    flex-direction: row;
    height: 36px;
    padding: 8px 12px;
    border-radius: 8px;
    gap: 2px;
    color: #6F77FE;
    font-weight: 600;
    font-size: 14px;
    line-height: 18px;
    text-align: center;
    background-color: #F4F4F6;
    cursor: pointer;
  }

  .cancel-choose {
    background-color: transparent;
  }

  .icon {
    width: 20px;
    height: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .selection-subtitle,
  .cancel-subtitle,
  .favorite-subtitle,
  .share-subtitle {
    padding: 1px 4px;
  }

  .actions {
    display: flex;
    flex-direction: row;
    gap: 8px;
  }
}

.header-container .container {
  margin-top: 94px;
}

@media (max-width: 743px) {
  .header-container .container {
    margin-top: 64px;
  }
}

@media (max-width: 743px) {
  .header-container.chosen {
    height: 64px;
  }
  
}

.header-container.chosen .container {
  margin-top: 64px;
}
</style>
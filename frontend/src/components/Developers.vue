<template>
  <div class="developers">
    <div class="developers-subtitle">
        Застройщики
    </div>
    <div class="status-legend">
      <div class="item">
        <div class="chip-color"><img src="@/assets/img/status-chip-selected.svg" alt="Выбрано"></div><span class="chip">Выбрано: {{ selectedCount }}</span>
      </div>
      <div class="item">
        <div class="chip-color"><img src="@/assets/img/status-chip-positive.svg" alt="Доступно"></div><span class="chip">Доступно: {{ availableCount }}</span>
      </div>
      <div class="item">
        <div class="chip-color"><img src="@/assets/img/status-chip-negative.svg" alt="Не уникальный"></div><span class="chip">Не уникальный клиент: {{ nonUniqueCount }}</span>
      </div>
      <div class="item">
        <div class="chip-color"><img src="@/assets/img/status-chip-none.svg" alt="Нет объектов"></div><span class="chip">Нет объектов: {{ noObjectsCount }}</span>
      </div>
    </div>
    <div class="developers-list">
      <button v-for="developer in developers" :key="developer.id" :class="getStatusClass(developer.status)" @click="toggleSelection(developer)" :disabled="developer.status === 'Нет объектов' || developer.status === 'Не уникальный клиент'">
        <img :src="developer.logo" :alt="developer.name">
      </button>
    </div>
  </div>
</template>
  
  <script>
  export default {
    name: 'Developers',
    data() {
      return {
        developers: [
            { id: 1, name: 'AFI', logo: require('@/assets/img/afi-logo.svg'), status: 'Выбрано' },
            { id: 2, name: 'AVA', logo: require('@/assets/img/ava-logo.svg'), status: 'Доступно' },
            { id: 3, name: 'Ambassadori Island', logo: require('@/assets/img/ambassadori-island-logo.svg'), status: 'Нет объектов' },
            { id: 4, name: 'Агой-парк', logo: require('@/assets/img/park-logo.svg'), status: 'Нет объектов' },
            { id: 5, name: 'АСИ', logo: require('@/assets/img/asi-logo.svg'), status: 'Доступно' },
            { id: 6, name: 'Континент', logo: require('@/assets/img/kontinent-logo.svg'), status: 'Нет объектов' },
            { id: 7, name: 'Семья', logo: require('@/assets/img/family-logo.svg'), status: 'Доступно' },
            { id: 8, name: 'Точно', logo: require('@/assets/img/exactly-logo.svg'), status: 'Доступно' },
            { id: 9, name: 'Флагман', logo: require('@/assets/img/flagman-logo.svg'), status: 'Нет объектов' },
            { id: 10, name: 'Юг-Инжиниринг', logo: require('@/assets/img/south-logo.svg'), status: 'Не уникальный клиент' },
        ]
      };
    },
    computed: {
      selectedCount() {
        return this.developers.filter(d => d.status === 'Выбрано').length;
      },
      availableCount() {
        return this.developers.filter(d => d.status === 'Доступно').length;
      },
      nonUniqueCount() {
        return this.developers.filter(d => d.status === 'Не уникальный клиент').length;
      },
      noObjectsCount() {
        return this.developers.filter(d => d.status === 'Нет объектов').length;
      }
    },
    methods: {
      checkUniqueness() {
        console.log('Проверка уникальности:', this.name, this.phone);
      },
      toggleSelection(developer) {
        if (developer.status === 'Выбрано') {
          developer.status = 'Доступно';
        } 
        else if (developer.status === 'Доступно') {
          developer.status = 'Выбрано';
        }
      },
      getStatusClass(status) {
        return {
          'developer-card selected': status === 'Выбрано',
          'developer-card available': status === 'Доступно',
          'developer-card non-unique': status === 'Не уникальный клиент',
          'developer-card no-objects': status === 'Нет объектов'
        };
      }
    }
  };
  </script>
  
  <style scoped>
    .developers-subtitle {
      font-weight: 600;
      font-size: 17px;
      color: #1E1E24;
      line-height: 22px;
      display: flex;
      padding-top: 18px;
      padding-left: 16px;
      padding-bottom: 10px;
      user-select: none;
    }

    .developers {
      padding: 0px 0px 8px;
      margin: 0px 8px;
      background-color: #FFFFFF;
      border-radius: 12px;
      display: flex;
      flex-direction: column;
      row-gap: 8px;
    }

    .chip-color {
      width: 20px;
      height: 20px;
      padding-right: 6px;
    }

    .item {
      padding: 4px 8px;
      height: 32px;
      border: 1px solid #DDDDE3;
      border-radius: 6px;
      background-color: #FFFFFF;
      display: flex;
      align-items: center;
      flex-direction: row;
      gap: 3px;
      user-select: none;
    }

    .chip {
      line-height: 1px;
    }

    .status-legend {
      display: flex;
      flex-wrap: wrap;
      gap: 4px;
      padding: 6px 8px;
    }

    .developers-list {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      padding: 6px 8px;
    }

    .developer-card {
      height: 48px;
      border-radius: 8px;
      padding: 12px;
      border: 2px solid #FFFFFF;
      cursor: pointer;
    }

    .developer-card img {
      user-select: none;
    }

    .selected {
      border: 2px solid #6F77FE;
      background-color: #FFFFFF;
    }

    .available {
      background-color: #F3FFF9;
    }

    .non-unique {
      background-color: #FFF8F7;
      cursor: default;
    }
    
    .no-objects {
      background-color: #FAFAFA;
      cursor: default;
    }

    .available:hover {
      box-shadow: 0px 8px 16px 0px #17171C0D;
      background-color: #FFFFFF;
    }

    .developer-card img {
      min-height: 24px;
      max-height: 24px;
      min-width: 66px;
      max-width: 66px;
    }

    @media (max-width: 431px) {
      .developers-list {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
      }
    }

    @media (max-width: 743px) {
      .developer-card {
        min-width: 90px;
      }
    }

    @media (min-width: 744px) and (max-width: 1023px) {
      .developer-card {
        min-width: 90px;
      }
    }

    @media (min-width: 1024px) {
      .developers {
        margin: 0;
        padding: 0;
        width: 100%;
      }

      .developers-list {
        height: 168px;
        scrollbar-gutter: stable;
        overflow-y: scroll;
        padding: 16px;
      }

      .developer-card {
        min-width: 120px;
        height: 64px;
      }

      .developers-list::-webkit-scrollbar {
        width: 8px;
        height: 76px;
        align-items: flex-start;
        display: flex;
      }

      .developers-list::-webkit-scrollbar-thumb {
        background: #B7B8C399;
        border-radius: 8px;
      }

      .developers-list::-webkit-scrollbar-track {
        background: transparent;
      }

      .developers-list::-webkit-scrollbar-button {
        display: none;
      }
    }
  </style>
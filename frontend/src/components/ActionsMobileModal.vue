<template>
    <div v-if="isOpen" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content">
        <p class="modal-title">
            <span class="info">{{ data.additionalInfo.name }}, №{{ data.number }}, {{ data.rooms }}-к, {{ data.pricePerMetr }} м²</span>
            <span class="price">{{ data.price }} ₽</span>
        </p>
        <ul class="modal-list">
          <li class="list-element" @click="action('Множественный выбор')">
                <span class="icon"><img src="@/assets/img/multi-select.svg" alt="Множественный выбор"></span> <div class="list-title">Множественный выбор</div>
            </li>
            <li class="list-element" @click="action('Добавить в избранное')" v-if="!data.isLiked">
                <span class="icon"><img src="@/assets/img/favorite.svg" alt="Избранное"></span> <div class="list-title">Добавить в избранное</div>
            </li>
            <li class="list-element" @click="action('Удалить из избранного')" v-if="data.isLiked">
                <span class="icon"><img src="@/assets/img/favorite-fill.svg" alt="Избранное"></span> <div class="list-title">Удалить из избранного</div>
            </li>
            <li class="list-element" @click="action('Добавить в подборки')">
                <span class="icon"><img src="@/assets/img/selection.svg" alt="Подборка"></span> <div class="list-title">Добавить в подборки</div>
            </li>
            <li class="list-element" @click="action('Зафиксировать')">
                <span class="icon"><img src="@/assets/img/fixed.svg" alt="Фиксация"></span> <div class="list-title">Зафиксировать</div>
            </li>
            <li class="list-element" @click.prevent="shareLink">
                <span class="icon"><img src="@/assets/img/share.svg" alt="Поделиться"></span> <div class="list-title">Поделиться</div>
            </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      isOpen: Boolean,
      data: Object
    },
    methods: {
      closeModal() {
        this.$emit("close");
      },
      action(name) {
        if (name ==='Множественный выбор') {
            this.$emit('addMultySelect')
        } else if (name === 'Добавить в избранное' || name === 'Удалить из избранного') {
            this.$emit('toggleFavourite')
        }
        this.closeModal();
      },
      shareLink() {
        let link = window.location.origin + '/card?id=' + this.data.id;
        window.navigator.clipboard.writeText(link)
      }
    },
    mounted() {
        console.log('Data:' , this.data, this.isOpen)
    }
  };
  </script>
  
  <style scoped>
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
        height: 320px;
        border-radius: 12px;
        border: 1px solid #ECEDF0;
        box-shadow: 0px 8px 16px 0px #17171C0D;
        margin-bottom: 8px;
    }
    
    .modal-title {
        margin-bottom: 0px;
        margin-top: 0px;
        height: 64px;
    }

    .info {
        font-weight: 600;
        font-size: 14px;
        line-height: 18px;
        color: #9596A7;
        display: flex;
        text-align: left;
        padding: 14px 16px 0px;
    }
  
    .price {
        font-weight: 400;
        font-size: 12px;
        line-height: 14px;
        color: #B7B8C3;
        text-align: left;
        display: flex;
        padding: 0px 0px 14px 16px;
    }
  
    .modal-list {
        list-style: none;
        padding: 0;
        margin-bottom: 8px;
        margin-top: 0px;
    }
    
    .modal-list li {
        height: 48px;
        padding: 0px 16px;
        display: flex;
        align-items: center;
        cursor: pointer;
    }
    
    .modal-list li .icon {
        margin-right: 8px;
    }
    
    .modal-list li:hover {
        background: #f0f0f0;
    }

    .icon {
      width: 24px;
      height: 24px;
      padding-right: 16px;
    }
  </style>
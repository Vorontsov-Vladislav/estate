<template>
    <div class="desktop-modal" v-if="isOpen" @click.self="closeModal">
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
            <li class="list-element" @click="shareLink">
                <span class="icon"><img src="@/assets/img/share.svg" alt="Поделиться"></span> <div class="list-title">Поделиться</div>
            </li>
        </ul>
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
    .desktop-modal {
        width: 276px;
        padding: 8px;
        z-index: 10;
        background-color: #FFFFFF;
        border: 1px solid #ECEDF0;
        border-radius: 12px;
        position: absolute;
        top: 40px;
        right: 10px;
    }

    .desktop-modal:hover {
        box-shadow: 0px 8px 16px 0px #17171C0D;
    }

    .modal-list li {
        list-style-type: none;
        width: 260px;
        padding: 6px 16px;
        align-items: center;
        cursor: pointer;
    }

    .icon {
        width: 24px;
        height: 24px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .list-element {
        display: flex;
        flex-direction: row;
        gap: 16px;
    }

    .list-title {
        height: 20px;
        font-weight: 500;
        font-size: 16px;
        line-height: 20px;
    }
</style>
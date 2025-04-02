<template>
    <form class="unique-check">
        <div class="unique-subtitle">
            Проверка уникальности
        </div>

        <div class="check-data">
            <div class="name">
                <label class="label-name" for="name">Имя <span class="required">*</span></label>
                <input type="text" id="name" v-model="name" placeholder="Игорь" required autocomplete="off">
            </div>
            <div class="phone">
                <label class="label-phone" for="phone">Телефон <span class="required">*</span></label>
                <input type="text" id="phone" v-model="phone" placeholder="+7(900)000-00-00" required v-mask="'+7(###)###-##-##'" autocomplete="off">
            </div>
            <div class="btn-group">
              <button class="button-check-unique" type="submit" @click="checkUniqueness">Проверить</button>
            </div>
        </div>
      </form>
</template>

<script>

export default {
    name: 'CheckUnique',
    data() {
      return {
        name: '',
        phone: '',
      }
    },
    methods: {
        checkUniqueness(event) {
          event.preventDefault();
          console.log('Проверка уникальности:', this.name, this.phone);
        }
    }
}
</script>

<style scoped>
    .required {
      font-weight: 400;
      font-size: 14px;
      line-height: 18px;
      color: #DB2F22;
      padding-left: 2px;
    }

    .unique-subtitle {
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

    .unique-check {
      background-color: #FFFFFF;
      margin: 8px 8px 0;
      padding-bottom: 8px;
      border-radius: 12px;
    }

    .check-data {
      padding: 8px 16px 0;
    }

    .check-data {
      display: flex;
      flex-direction: column;
    }

    .name, .phone {
      margin-bottom: 15px;
    }

    .label-name, .label-phone {
      display: flex;
      user-select: none;
    }

    .label-name,
    .label-phone {
      padding: 6px 0px;
      font-weight: 400;
      font-size: 14px;
      line-height: 18px;
      color: #9596A7;
    }

    input[type="text"] {
      width: 100%;
      border: 1px solid #DDDDE3;
      border-radius: 8px;
      box-sizing: border-box;
      color: #000000;
      padding: 6px 12px;
      outline: none;
      user-select: none;
    }

    .button-check-unique {
      background-color: #6F77FE;
      border-radius: 8px;
      height: 36px;
      padding: 8px 12px;
      width: 100%;
      color: #FFFFFF;
      font-weight: 600;
      font-size: 14px;
      line-height: 18px;
      border: 1px solid;
      user-select: none;
      cursor: pointer;
    }

    .btn-group {
      height: 48px;
      display: flex;
      align-items: center;
    }

    @media (min-width: 1024px) {
      .unique-check {
        min-width: 360px;
        margin: 0;
      }
    }
</style>
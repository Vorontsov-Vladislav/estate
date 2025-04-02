<template>
    <div class="card-container">
        <div class="card-header">
            <div class="size">
                <div class="count-rooms">
                    {{ data.rooms }}-к,
                </div>
                <div class="square">
                    {{ data.square }} <span class="square-value">м²</span>
                </div>
            </div>

            <div class="number">№ {{ data.number }} </div>
            <div class="menu">
                <img @click="showModal" src="@/assets/img/actions.svg" alt="Меню" v-if="!isMultyActive">
                <input 
                    type="checkbox" 
                    name="" id="" 
                    v-if="isMultyActive" 
                    v-model="isChosen"
                    @click="chooseFlat"
                >
                <ActionsMobileModal 
                    v-if="isMobileModalOpen" 
                    :isOpen="isMobileModalOpen" 
                    :data="data" 
                    @close="isMobileModalOpen = false" 
                    @addMultySelect="()=>{isChosen = true; $emit('addObjectToSelected', data.id)}"
                    @toggleFavourite="$emit('onToggleFavourite', data.id)"
                />
                <ActionsDesktopModal 
                    v-if="isDesktopModalOpen" 
                    :isOpen="isDesktopModalOpen" 
                    :data="data" 
                    @close="isDesktopModalOpen = false" 
                    @addMultySelect="()=>{isChosen = true; $emit('addObjectToSelected', data.id)}"
                    @toggleFavourite="$emit('onToggleFavourite', data.id)"
                />
            </div>
        </div>
        
        <div class="card-body">
            <div class="img-block">
                <ul 
                    class="slider" 
                    v-if="data.images.length"
                    @mouseover="()=>{slideShowStatus=true;}"
                    @mouseleave="()=>{slideShowStatus=false; photoShownInd=0;}"
                >
                    <li 
                        class="slider-column" 
                        v-for="ind in data.images.length" 
                        :key="ind"
                        @mouseover="()=>{photoShownInd=ind-1;}"
                    ></li>
                </ul>
                <img src="@/assets/img/card-no-image.svg" alt="Нет изображения планировки" v-if="!data.images.length" class="photo">
                <img :src=" data.images[photoShownInd].path" alt="Планировка" v-else class="photo" @touchstart="touchStartFunc" @touchend="touchEndFunc">
                <ul class="slider-dots">
                    <li 
                        class="slider-dots__dot"
                        :class="[photoShownInd===ind-1?'slider-dots__dot-active':'']"
                        v-for="ind in data.images.length" 
                        :key="ind"
                        @click="()=>{photoShownInd=ind-1}"
                    ></li>
                </ul>
            </div>
            <div class="info">
                <div class="price">
                    {{ data.price }} ₽
                </div>
                <div class="price-per-metr">
                    {{ data.pricePerMetr }} ₽/м²
                </div>
                <div class="additional-info">
                    <div class="city">
                        {{ data.additionalInfo.city }}
                        <div class="separator"><img src="@/assets/img/separator.svg" alt="Разделитель"></div>
                    </div>
                    <div class="name">
                        {{ data.additionalInfo.name }}
                        <div class="separator"><img src="@/assets/img/separator.svg" alt="Разделитель"></div>
                    </div>
                    <div class="litter">
                        Литер {{ data.additionalInfo.litter }}
                        <div class="separator"><img src="@/assets/img/separator.svg" alt="Разделитель"></div>
                    </div>

                    <div class="entrance">
                        Подъезд {{ data.additionalInfo.entrance }}
                        <div class="separator"><img src="@/assets/img/separator.svg" alt="Разделитель"></div>
                    </div>

                    <div class="floor">
                        Этаж {{ data.additionalInfo.currentFloor }} из {{ data.additionalInfo.maxFloor }}
                        <div class="separator"><img src="@/assets/img/separator.svg" alt="Разделитель"></div>
                    </div>

                    <div class="living-area">
                        Жилая площадь {{ data.additionalInfo.livingArea }} м²
                    </div>
                </div>
            </div>
        </div>

        <div class="card-footer">
            <div class="company-logo">
                <img :src="data.logo" alt="Логотип компании">
            </div>
            <div class="promo" v-if="data.promo">
                <img src="@/assets/img/promo.svg" alt="Промо">
            </div>
        </div>
    </div>
</template>

<script>
    import ActionsMobileModal from "./ActionsMobileModal.vue";
    import ActionsDesktopModal from "./ActionsDesktopModal.vue";
    export default {
        name: 'Card',
        components: { 
            ActionsMobileModal,
            ActionsDesktopModal
         },
        props: {
            data: Object,
            isMultyActive: Boolean
        },
        data() {
            return {
                photoShownInd: 0,
                slideShowStatus: false,
                isMobileModalOpen: false,
                isDesktopModalOpen: false,
                touchStartX: 0,
                touchEndX: 0,
                isChosen: false
            }
        },
        watch: {
            isMultyActive(newVal) {
                if (!newVal) {
                    this.isChosen = false;
                }
            }
        },
        methods: {
            showModal() {
                if (window.innerWidth <= 743) {
                    this.isMobileModalOpen = true;
                } else {
                    this.isDesktopModalOpen = !this.isDesktopModalOpen;
                }
            },
            touchStartFunc (event) {
                this.touchStartX = event.changedTouches[0].screenX;
            },
            touchEndFunc (event) {
                this.touchEndX = event.changedTouches[0].screenX;
                if (this.touchEndX < this.touchStartX && this.photoShownInd < this.data.images.length-1) {
                    this.photoShownInd++;
                } else if (this.touchEndX > this.touchStartX && this.photoShownInd > 0) {
                    this.photoShownInd--;
                }
            },
            chooseFlat () {
                if (this.isChosen) {
                    this.$emit('deleteObjectFromSelected', this.data.id)
                } else {
                    this.$emit('addObjectToSelected', this.data.id)
                }
            }
        },
        mounted () {
            this.isChosen = this.data.isChosen;            
        }
    }
</script>

<style scoped>
    .card-container {
        border-radius: 12px;
        background-color: #FFFFFF;
        padding-top: 8px;
        padding-bottom: 24px;
    }

    .card-container:hover {
        box-shadow: 0px 8px 16px 0px #17171C0D;
    }

    .card-header {
        height: 70px;
        padding: 0 16px;
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        row-gap: 4px;
    }

    .count-rooms, .square {
        height: 24px;
    }

    .size {
        display: flex;
        flex-wrap: wrap;
        flex-direction: row;
        font-weight: 600;
        font-size: 20px;
        line-height: 24px;
        gap: 5px;
        color: #1E1E24;
    }

    .menu {
        width: 48px;
        height: 48px;
        display: flex;
        position: absolute;
        top: 0px;
        right: 0px;
        justify-content: center;
        align-items: center;
    }

    .menu img {
        width: 4px;
        height: 16px;
        cursor: pointer;
    }

    .number {
        text-align: left;
        font-weight: 400;
        font-size: 14px;
        line-height: 18px;
        color: #9596A7;
    }

    .info {
        margin: 0px 16px 16px;
    }

    .additional-info {
        display: flex;
        flex-wrap: wrap;
        flex-direction: row;
        gap: 8px;
        align-items: center;
        font-weight: 400;
        font-size: 14px;
        line-height: 18px;
    }

    .price {
        display: flex;
        font-weight: 600;
        font-size: 24px;
        line-height: 28px;
        color: #1E1E24;
        text-align: left;
        margin-bottom: 4px;
    }

    .price-per-metr {
        display: flex;
        font-weight: 400;
        font-size: 14px;
        line-height: 18px;
        color: #9596A7;
        text-align: left;
        height: 18px;
        margin-bottom: 12px;
    }

    .city,
    .name,
    .litter,
    .floor,
    .entrance,
    .living-area {
        display: flex;
    }

    .separator {
        display: flex;
        margin-left: 8px;
        align-items: center;
    }

    .separator img {
        width: 2px;
        height: 2px;
    }

    .card-footer {
        display: flex;
        flex-direction: row;
        padding: 0px 16px;
        justify-content: space-between;
    }

    .promo {
        width: 48px;
        height: 48px;
        border-radius: 50%;
        background-color: #6F77FE;
        display: flex;
        align-items: center;
    }

    .promo img {
        display: flex;
        width: 14px;
        height: 20px;
        margin: auto;
    }

    /* slider */
    .img-block {
        position: relative;
        width: 100%;
        padding: 0 16px;
    } 
    .slider {
        list-style-type: none;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: row;
        column-gap: 5px;
        height: 190px;
    } 

    .slider-column {
        height: 100%;
        width: 100%;
    } 

    .photo {
        width: 100%;
        object-fit: cover;
        height: 190px;
    }

    .slider-dots {
        display: flex;
        flex-direction: row;
        column-gap: 8px;
        list-style-type: none;
        width: 100%;
        justify-content: center;
        height: 32px;
        padding-top: 16px;
    }

    .slider-dots__dot {
        width: 8px;
        height: 8px;
        background: #DDDDE3;
        border-radius: 50%;
        cursor: pointer;
    }

    .slider-dots__dot-active {
        background: #6F77FE;
    }

    /*  */
    .card-header,
    .card-body,
    .card-footer {
        user-select: none;
    }

    input[type="checkbox"] {
        margin: 0px;
        width: 18px;
        height: 18px;
        accent-color: #6F77FE;
    }

    input[type="checkbox"]:not(:checked) {
        border: 10px solid #FF0000; 
    }

    @media (max-width: 743px) {
        .card-container {
            margin: 0px auto 16px;
            min-width: 304px;
            max-width: 320px;
        }
    }

    @media (min-width: 744px) and (max-width: 1023px) {
        .card-container {
            min-width: 304px;
            max-width: 326px;
        }
    }

    @media (min-width: 1024px) and (max-width: 1365px) {
        .card-container {
            min-width: 304px;
            max-width: 320px;
        }
    }

    @media (min-width: 1024px) {
        .card-container {
            min-width: 304px;
            max-width: 420px;
        }
    }

    @media (max-width: 1365px) {
        .slider {
            display: none;
        }
    }
</style>
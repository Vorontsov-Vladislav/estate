<template>
    <div class="card">
        <Card 
            v-for="flat in flatsShown" 
            :key="flat.id" 
            :data="flat" 
            :isMultyActive="isMultyActive"
            @addObjectToSelected="chooseFlat"
            @deleteObjectFromSelected="deleteFlatFromChosen"
            @onToggleFavourite="toggleFavourite"
            />
        <div class="loader">
            <button class="load-more-btn" @click="loadMore" v-if="loadMoreButtonShow">Показать ещё {{ flatsLeft }} объектов из {{ totalFlats }}</button>
        </div>
    </div>
</template>

<script>
    import Card from "./Card.vue";
    export default {
        props: {
            isMultyActive: Boolean
        },
        name: 'CardGrid',
        components: {
            Card
        },
        data() {
            return {
                flats: [
                    { id: 1, rooms: "0", square: '0 000.00', number: '0000', 
                        images: [], price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-afi.svg'), promo: true },
                    { id: 2, rooms: "0", square: '0 000.00', number: '0000', 
                        images: [
                            { id: 1, path: require('@/assets/img/plain-2.svg') },
                            { id: 2, path: require('@/assets/img/plain-3.svg') },
                            { id: 3, path: require('@/assets/img/plain-4.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-ava.svg'), promo: true },
                    { id: 3, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-3.svg') },
                            { id: 2, path: require('@/assets/img/plain-3.svg') },
                            { id: 3, path: require('@/assets/img/plain-3.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-family.svg'), promo: true },
                    { id: 4, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-4.svg') },
                            { id: 2, path: require('@/assets/img/plain-4.svg') },
                            { id: 3, path: require('@/assets/img/plain-4.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-ava.svg'), promo: false },
                    { id: 5, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-5.svg') },
                            { id: 2, path: require('@/assets/img/plain-5.svg') },
                            { id: 3, path: require('@/assets/img/plain-5.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-afi.svg'), promo: false },
                    { id: 6, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-6.svg') },
                            { id: 2, path: require('@/assets/img/plain-6.svg') },
                            { id: 3, path: require('@/assets/img/plain-6.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-ava.svg'), promo: false },
                    { id: 7, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-7.svg') },
                            { id: 2, path: require('@/assets/img/plain-7.svg') },
                            { id: 3, path: require('@/assets/img/plain-7.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-ava.svg'), promo: false },
                    { id: 8, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-8.svg') },
                            { id: 2, path: require('@/assets/img/plain-8.svg') },
                            { id: 3, path: require('@/assets/img/plain-8.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-family.svg'), promo: false },
                    { id: 9, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-9.svg') },
                            { id: 2, path: require('@/assets/img/plain-9.svg') },
                            { id: 3, path: require('@/assets/img/plain-9.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-ava.svg'), promo: false },
                    { id: 10, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-10.svg') },
                            { id: 2, path: require('@/assets/img/plain-10.svg') },
                            { id: 3, path: require('@/assets/img/plain-10.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-afi.svg'), promo: false },
                    { id: 11, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-11.svg') },
                            { id: 2, path: require('@/assets/img/plain-11.svg') },
                            { id: 3, path: require('@/assets/img/plain-11.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-afi.svg'), promo: false },
                    { id: 12, rooms: "0", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-12.svg') },
                            { id: 2, path: require('@/assets/img/plain-12.svg') },
                            { id: 3, path: require('@/assets/img/plain-12.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-family.svg'), promo: false },
                        { id: 13, rooms: "1", square: '0 000.00', number: '0000',
                        images: [
                            { id: 1, path: require('@/assets/img/plain-2.svg') },
                            { id: 2, path: require('@/assets/img/plain-3.svg') },
                            { id: 3, path: require('@/assets/img/plain-4.svg') }
                        ],
                        price: '000 000 000', pricePerMetr: '0 000 000', 
                        additionalInfo: {city: 'Краснодар', name: 'ЖК «ITRIELT»', litter: '0', 
                        entrance: '0', currentFloor: '00', maxFloor: '00', livingArea: '0 000.00'},
                        logo: require('@/assets/img/card-logo-family.svg'), promo: false },
                ],
                flatsShown: [],
                pageNumber: 0,
                pageSize: 3,
                flatsLeft: 0,
                totalFlats: 0,
                loadMoreButtonShow: true
            }
        },
        watch: {
            isMultyActive(newVal) {
                console.log('fire')
                if (!newVal) {
                    this.flatsShown.forEach((element) => {
                        element.isChosen = false;
                    }) 
                }
            }
        },
        methods: {
            loadMore () {
                this.pageNumber++;
                for (let i = this.pageSize*this.pageNumber; i < this.pageSize*this.pageNumber+this.pageSize; i++) {
                    this.flatsShown.push(
                    {
                        ...this.flats[i],
                        isChosen: false,
                        isLiked: false
                    }
                );
                    if (i === this.flats.length-1) {
                        break
                    }
                }
                this.flatsLeft = this.flatsShown.length + this.pageSize < this.flats.length ? this.pageSize : this.flats.length - this.flatsShown.length;
                this.checkButtonVis();
            },
            checkButtonVis () {
                if (this.flatsShown.length === this.flats.length) {
                    this.loadMoreButtonShow = false;
                }
            },
            chooseFlat (id) {                
                this.flatsShown.forEach((element) => {
                    if (element.id === id) {
                        element.isChosen = true;
                    }
                });
                this.$emit('addObjectToSelected', id);
            },
            deleteFlatFromChosen (id) {
                this.flatsShown.forEach((element) => {
                    if (element.id === id) {
                        element.isChosen = false;
                    }
                });
                this.$emit('deleteObjectFromSelected', id);
            },
            toggleFavourite (id) {
                this.flatsShown.forEach((element) => {
                    if (element.id === id) {
                        element.isLiked = !element.isLiked;
                    }
                });
            }
        },
        mounted () {
            for (let i = 0; i < this.pageSize; i++) {
                this.flatsShown.push(
                    {
                        ...this.flats[i],
                        isChosen: false,
                        isLiked: false
                    }
                );
            }            
            this.totalFlats = this.flats.length;
            this.flatsLeft = this.flatsShown.length + this.pageSize < this.flats.length ? this.pageSize : this.flats.length - this.flatsShown.length;
            this.checkButtonVis();
        },
    }
</script>

<style scoped>
    .card {
        margin: 16px 8px;
    }

    .loader {
        width: 100%;
        height: 80px;
        user-select: none;
    }

    .load-more-btn {
        margin: auto;
        border-radius: 8px;
        padding: 12px 20px;
        background-color: #6F77FE;
        color: #FFFFFF;
        border: 0px;
        font-weight: 500;
        font-size: 16px;
        line-height: 20px;
        text-align: center;
    }

    .load-more-btn:hover {
        cursor: pointer;
    }

    @media (max-width: 743px) {
        .card {
            display: flex;
            flex-direction: column;
            flex-wrap: nowrap;
        }
    }

    @media (min-width: 744px) and (max-width: 1023px) {
        .card {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            gap: 16px;
            align-items: center;
        }
    }

    @media (min-width: 1024px) and (max-width: 1365px) {
        .card {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            gap: 16px;
            align-items: center;
        }

        .card-container {
            min-width: 304px;
            max-width: 320px;
        }
    }

    @media (min-width: 1024px) {
        .card {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            gap: 16px;
            align-items: center;
        }

        .card-container {
            min-width: 304px;
            max-width: 420px;
        }
    }
</style>
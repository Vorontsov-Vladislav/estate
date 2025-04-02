<template>
  <div id="app">
    <Header 
      class="ml-80" 
      :chosenItemsCount="selectedFlats.length" 
      :isMultyActive="isMultyActive"
      @cancelMultyChoose="()=>{isMultyActive=false; selectedFlats = []}"
    > </Header>
    <MobileNavbar v-if="typeDevice !== 'Desktop'"></MobileNavbar>
    <DesktopNavbar v-else></DesktopNavbar>
    <div class="container ml-80" :class="!isMultyActive ? 'pt-94' : ''">
      <div class="inner-container">
        <CheckUnique></CheckUnique>
        <Developers></Developers>
      </div>
      <Info />
      <CardGrid 
        :isMultyActive="isMultyActive"
        @addObjectToSelected="addObjectToSelected"
        @deleteObjectFromSelected="deleteObjectFromSelected"
        @turnMultyChoose="()=>{isMultyActive=true;}"
      />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import CheckUnique from './components/CheckUnique.vue'
import Developers from './components/Developers.vue'
import Info from './components/Info.vue'
import CardGrid from './components/CardGrid.vue'
import MobileNavbar from './components/MobileNavbar.vue'
import DesktopNavbar from './components/DesktopNavbar.vue'

export default {
  name: 'App',
  components: {
    Header,
    CheckUnique,
    Developers,
    Info,
    CardGrid,
    MobileNavbar,
    DesktopNavbar
  },
  data() {
    return {
        typeDevice: '',
        selectedFlats: [],
        isMultyActive: false
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

        if (window.innerWidth >= 1366) {
            this.typeDevice = 'Desktop';
        }
    },
    addObjectToSelected (id) {      
      if (!this.isMultyActive) this.isMultyActive = true;
      this.selectedFlats.push(id);
    },
    deleteObjectFromSelected (id) {
      this.selectedFlats = this.selectedFlats.filter(element => element !== id);
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

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

h1,
h2,
h3,
h4,
h5,
h6,
p,
ul,
ol,
li,
blockquote {
  margin: 0;
  padding: 0;
}

body {
  margin: 0px;
}

.container {
  background-color: #FAFAFA;
  display: flex;
  flex-direction: column;
  row-gap: 8px;
  padding-top: 64px;
}

@media (max-width: 1023px) {
  .inner-container {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
}

@media (min-width: 1024px) {
  .inner-container {
    display: flex;
    flex-direction: row;
    gap: 16px;
    padding: 16px;
    border-bottom: 1px solid #ECEDF0;
  }
}

@media (min-width: 1366px) {
  .ml-80 {
    margin-left: 80px;
  }
}

@media (max-width: 743px)  {
  .pt-94 {
    padding-top: 94px;
  }
}
</style>

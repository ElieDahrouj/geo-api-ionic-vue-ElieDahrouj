<template>
  <div id="app">
    <ion-tabs>
      <ion-tab tab="/">
        <Commune/>
      </ion-tab>

      <ion-tab tab="district">
        <District/>
      </ion-tab>

      <ion-tab tab="region">
        <Region/>
      </ion-tab>

      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="/">
          <ion-label>Commune</ion-label>
          <ion-icon name="ios-navigate"></ion-icon>
        </ion-tab-button>

        <ion-tab-button tab="district">
          <ion-label>Département</ion-label>
          <ion-icon name="ios-pin"></ion-icon>
        </ion-tab-button>

        <ion-tab-button tab="region">
          <ion-label>Régions</ion-label>
          <ion-icon name="ios-map"></ion-icon>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </div>
</template>
<script>
    import Commune from '@/components/Home.vue'
    import District from '@/components/district.vue'
    import Region from '@/components/region.vue'
    export default {
        components: {
            Commune,
            District,
            Region
        }
    }
</script>
<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

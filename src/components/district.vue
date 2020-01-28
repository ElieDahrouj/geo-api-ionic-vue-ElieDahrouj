<template>
  <div class="ion-page">
    <Header title="Départements"/>

    <ion-content  class="ion-padding">
      <img style="width: 200px;" alt="Vue logo" src="../assets/district.jpg">

      <ion-item>
        <ion-label>Selectionnez un département </ion-label>
        <ion-select @ionChange="zipcode = $event.target.value">
          <ion-select-option v-for="(number) in department" :value="number.departmentCode">{{number.departmentName}}</ion-select-option>
        </ion-select>
      </ion-item>

      <div class="ion-padding">
        <ion-button @click.prevent="send()" expand="block" type="submit" class="ion-no-margin">Cherchez</ion-button>
      </div>
      <ion-list v-for="(t) in info">
        {{t.nom}}
      </ion-list>
    </ion-content>
  </div>
</template>

<script>
    import Header from '@/components/header.vue'
    import District from '../assets/ressource/district.json'
    export default {
        name: "district",
        components: {
            Header
        },
        data(){
            return {
                zipcode:null,
                department: District,
                info:[]
            }
        },
        methods:{
            send(){
                const district = this.department.map((element) => element.departmentCode)
                if (district.indexOf(this.zipcode) !== -1) {
                    this.$http.get('https://geo.api.gouv.fr/departements/' + this.zipcode + '/communes',)
                        .then(response => {
                            this.info = response.data
                        })
                }
                else {
                    this.alert()
                }
            },
            alert (){
                return this.$ionic.alertController.create({
                    header: 'Erreur',
                    message: "Aucune correspondance trouvée",
                    buttons: ['Ok']
                }).then(alert =>
                    alert.present()
                );
            }
        },
    };
</script>
<style>
  div ~ ion-list {
    border-bottom: 1px solid black;
  }
</style>
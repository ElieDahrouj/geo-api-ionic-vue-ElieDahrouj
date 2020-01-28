<template>
  <div class="ion-page">
    <Header title="Communes"/>

    <ion-content class="ion-padding">
      <img alt="Vue logo" src="../assets/welcome.png">
      <ion-item>
        <ion-label position="stacked" >Entrez une commune <ion-text color="danger">*</ion-text></ion-label>
        <ion-input type="text" @input="zipcode = $event.target.value"></ion-input>
      </ion-item>

      <div class="ion-padding">
        <ion-button @click.prevent="send()" expand="block" type="submit" class="ion-no-margin">Cherchez</ion-button>
      </div>

      <ion-card v-for="(t) in information">
        <ion-card-header>
          <ion-card-subtitle><b>Code:</b> {{t.code}}</ion-card-subtitle>
          <ion-card-title>{{t.nom}}</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <p><b>Population: </b>{{t.population}}</p>
          <p><b>Code Département: </b>{{t.codeDepartement}}</p>
          <p><b>Code région: </b>{{t.codeRegion}}</p>
        </ion-card-content>
      </ion-card>
    </ion-content>
  </div>
</template>

<script>
    import Header from '@/components/header.vue'
    export default {
        name: "home",
        components: {
            Header
        },
        data(){
            return {
                zipcode:null,
                information:[],
            }
        },
        methods:{
            send(){
                if(this.zipcode != null) {
                    if (parseInt(this.zipcode)) {
                        this.$http.get('https://geo.api.gouv.fr/communes?codePostal=' + this.zipcode,)
                            .then(response => {
                                if (response.data.length !== 0) {
                                    this.information = []
                                    response.data.forEach(doc => {
                                        this.information.unshift(doc)
                                    })
                                }
                                else {
                                    this.alert()
                                }
                            })
                    }
                    else {
                        if (!this.zipcode.match(/[0-9]+/g)) {
                            this.$http.get('https://geo.api.gouv.fr/communes?nom=' + this.zipcode,)
                                .then(response => {
                                    if (response.data.length !== 0) {
                                        this.information = []
                                        response.data.forEach(doc => {
                                            this.information.unshift(doc)
                                        })
                                    }
                                    else {
                                        this.alert()
                                    }
                                })
                        }
                        else {
                            this.alert()
                        }
                    }
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
        }
    };

</script>
<template>
    <div class="ion-page">
        <Header title="Régions"/>

        <ion-content  class="ion-padding">
            <img style="width: 270px;" alt="Vue logo" src="../assets/8867597.png">
            <ion-item>
                <ion-label>Selectionnez une région </ion-label>
                <ion-select @ionChange = "zipcode = $event.target.value">
                    <ion-select-option  v-for="(number) in regions" :value="number.regionCode">{{number.regionName}}</ion-select-option>
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
    import Regions from '../assets/ressource/regions.json'
    export default {
        components: {
            Header
        },
        data(){
            return {
                zipcode:null,
                info:[],
                regions : Regions
            }
        },
        methods:{
            send(){
                const regions = this.regions.map((element) => element.regionCode)
                if (regions.indexOf(this.zipcode) !== -1) {
                    this.$http.get('https://geo.api.gouv.fr/regions/' + this.zipcode + '/departements',)
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
        }
    };

</script>
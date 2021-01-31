<template>
    <div>
        <ion-card class="ion-text-center" v-if="rate">
            <ion-card-header>
                <ion-card-subtitle>{{ search.money}} EUR = </ion-card-subtitle>
                <ion-card-title>{{ convertedMoney }} {{ search.devise }}</ion-card-title>
            </ion-card-header>
        </ion-card>
    </div>
</template>

<script>
    import { IonCard, IonCardHeader, IonCardTitle, IonCardSubtitle } from '@ionic/vue';

    export default {
        name: "Results",
        components: [
            IonCard,
            IonCardHeader,
            IonCardTitle,
            IonCardSubtitle
        ],
        props: ['search'],
        methods: {
            getRates(){
                fetch(`http://data.fixer.io/api/latest?access_key=${process.env.VUE_APP_KEY_API}&symbols=${this.search.devise}`)
                .then(res => res.json())
                .then(json => {
                    this.rate = json.rates[this.search.devise];
                    this.convertedMoney = this.search.money * this.rate;
                    this.convertedMoney = Math.round(this.convertedMoney * 100) / 100;
                })
            }
        },
        mounted() {
            this.getRates();
        },
        data(){
            return{
                rate:false,
                convertedMoney: null
            }
        },
        watch: {
            search: {
                deep: true,
                handler(){
                    this.getRates();
                }
            }
        },
    }
</script>

<style scoped>

</style>
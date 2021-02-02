<template>
    <div>
        <ion-grid>
            <ion-row class="ion-align-items-center">
                <ion-col size="8">
                <ion-item class="custom-item-input">
                    <ion-input type="number" autofocus placeholder="Montant" v-model="options.money"></ion-input>
                    <ion-label>€</ion-label>
                </ion-item>
                </ion-col>
                <ion-col size="4">
                <ion-item>
                    <ion-select v-model="options.devise" placeholder="Devise" interface="action-sheet">
                        <ion-select-option v-for="(text,symbol) in devises" :key="text" :value="symbol">{{ text }}</ion-select-option>
                    </ion-select>
                </ion-item>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
                    <ion-button :disabled="!options.money || !options.devise" @click="$emit('convert', options )" expand="block">Convertir</ion-button>
                </ion-col>
            </ion-row>
        </ion-grid>    
    </div>
</template>

<script>
    import { IonInput, IonItem, IonSelect, IonSelectOption, IonGrid, IonRow, IonCol, IonLabel, IonButton } from '@ionic/vue';
 
    export default {
        data(){
            return {
                devises: [],
                options: {
                    money:"",
                    devise: ""
                },
                money:""
            }
        },
        name: "Search",
        components: {
            IonInput, 
            IonItem,  
            IonSelect, 
            IonSelectOption,
            IonGrid,
            IonRow,
            IonCol,
            IonLabel,
            IonButton
        },
        mounted(){
            fetch(`http://data.fixer.io/api/symbols?access_key=${process.env.VUE_APP_KEY_API}`)
            .then(res => res.json())
            .then(json => {
                this.devises = json.symbols;
                })
        }
    }
</script>

<style scoped>

</style>
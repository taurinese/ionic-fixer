<template>
  <ion-page>
    <ion-header collapse="condense">
      <ion-toolbar>
        <ion-title size="large" class="ion-text-center">ionic-fixer</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-grid>
        <ion-row class="ion-align-items-center">
          <ion-col>
            <Search @convert="getData"></Search>
            <Results v-if="search.money" :search="search"></Results>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol } from '@ionic/vue';
import Search from "@/components/Search.vue";
import Results from "@/components/Results.vue";

export default({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    Search,
    Results,
    IonGrid,
    IonRow,
    IonCol
  },
  methods: {
    getData(options){
      this.search.money = options.money;
      this.search.devise = options.devise;
    }
  },
  data(){
    return {
      search: {
        money: false,
        devise:false
      }
    }
  }
});
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}

ion-content {
  --offset-bottom: auto!important;
  --overflow: hidden;
  overflow: auto;
}

ion-content::-webkit-scrollbar {
    display: none;
}

ion-row {
  height:90vh;

}

ion-header{
  height: 5vh;
}

</style>
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Team</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content v-if="state.loading">
      <div class="loading-center">
        <ion-spinner color="primary"></ion-spinner>
      </div>
    </ion-content>
    <ion-content v-else :fullscreen="true">
      <ion-refresher slot="fixed" @ionRefresher="doRefresh">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>
      <PremierCard :team="state.PremierTeams"></PremierCard>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent,IonSpinner,IonRefresher, IonRefresherContent,
 } from '@ionic/vue';
import axios from 'axios';
import{reactive} from 'vue';
import IPremierTeams from '../interfaces/IPremierTeams';
import PremierCard from '@/components/PremierCard.vue';

export default  {
  name: 'Tab1',
  components: {  IonHeader, IonToolbar, IonTitle, IonContent, IonPage,IonSpinner,IonRefresher, IonRefresherContent,PremierCard 
  },
  setup(){
    const state= reactive({
      PremierTeams:{} as IPremierTeams,
      loading:false,
    });

    const fetchPremierTeams = async (displayLoaderPage: boolean)=>{
      if(displayLoaderPage){
        state.loading =true;
      }

      const res= await axios.get(
        "https://www.thesportsdb.com/api/v1/json/1/search_all_teams.php?l=English%20Premier%20League"
      );

      if(res.data){
        state.PremierTeams=res.data?.teams[0];
      }
      state.loading = false;
    };

    const doRefresh = (event: CustomEvent) => {
      fetchPremierTeams(false);
      // eslint-disable-next-line @typescript-eslint/ban-ts-ignore
      //@ts-ignore
      event.target?.complete();
    };
    
    fetchPremierTeams(true);
    return{
      state,
      fetchPremierTeams,
      doRefresh
    }
  }
}
</script>
<style scoped>
.loading-center{
  display:flex;
  align-items:center;
  justify-content:center;
  height: 90vh;
}
ion-spiner{
  transform: scale(1.5);
}
</style>
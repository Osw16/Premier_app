<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>PL Teams</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content v-if="state.loading">
      <div class="loading-center">
        <ion-spinner color="primary"></ion-spinner>
      </div>
    </ion-content>

    <ion-content :fullscreen="true" v-else>
      <ion-list>
        <ion-item
        v-for="team in state.lstTeams"
        :key="team.strTeam"
        @click="
        ()=>
        router.push(`/premier-table/${team.strTeam}`)  
        "
        >
        <ion-avatar slot="start">
          <img :src="teamBadge(team.strTeam)">
        </ion-avatar>

        <ion-label>
          <h2>{{team.strTeam}}</h2>
        </ion-label>
        </ion-item>

      </ion-list>
    </ion-content>

    <ion-content>
      
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonSpinner, IonAvatar, IonLabel, IonItem, IonList } from '@ionic/vue';
import IPremierTeams from '../interfaces/IPremierTeams';
import {reactive} from 'vue';
import axios from 'axios';
import {useRouter} from 'vue-router';

export default  {
  name: 'Tab2',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage,IonSpinner, IonAvatar, IonLabel, IonItem, IonList 
  },
  setup(){
  const router = useRouter();
  const state = reactive({
    lstTeams:[] as IPremierTeams[],
    loading:false
  });
  const fetchTable=async()=>{
    state.loading=true;
    const res = await axios.get(
      "https://www.thesportsdb.com/api/v1/json/1/search_all_teams.php?l=English%20Premier%20League"
    );
    if(res.data){
      state.lstTeams = res.data.teams;
      state.lstTeams.sort(function(a,b){
        return a.strTeam.localeCompare(b.strTeam);
      });
      state.loading=false;
    }

  }
    const teamBadge=(badge: string)=>{
      const myRegexito: RegExp = new RegExp();
      return badge = `https://www.thesportsdb.com/images/media/team/badge/`.(/[\w-]+.(jpg|png|txt)/g)
       
    }
    // const teamBadge=(strTeamBadge: string)=>{
    //   return `https://www.thesportsdb.com/images/media/team/badge/uyhbfe1612467038.png`
    // }

   
    fetchTable();
    return{
      router,
      state,
      teamBadge
    }
  }
  
}

</script>
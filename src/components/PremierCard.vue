<template>

      <ion-card>
        <img :src="team.strStadiumThumb" />

        <ion-card-header>
          <ion-card-subtitle>
            {{ team.strTeam }} | At
            {{ team.strStadium }}
          </ion-card-subtitle>

          <ion-card-title>{{ team.strStadium }}</ion-card-title>
        </ion-card-header>

        <ion-card-content>
          <p>{{ team.strTeam }}</p>
          <ion-list-header>
            <ion-label>Ingredients</ion-label>
          </ion-list-header>

          
          <ion-list>
            <template v-for="index in 20" :key="index">
              <ion-item v-if="team[`strTeam${index}`]">
                <ion-label>
                  <span v-if="team[`stTeam${index}`]">
                    {{ team[`strTeam${index}`] }}
                  </span>
                    {{team[`strTeam${index}`]}}
                </ion-label>
              </ion-item>
            </template>
          </ion-list>

        </ion-card-content>
      </ion-card>
  
</template>

<script script="ts">
import {IonCard,IonCardHeader,IonCardSubtitle,IonCardContent,IonCardTitle,IonList,IonListHeader,IonLabel,IonItem
} from '@ionic/vue';

export default {
    name:'PremierCard',
    props:{
        team:Object,
    },
    components:{
        IonCard,
        IonCardHeader,
        IonCardSubtitle,
        IonCardContent,
        IonCardTitle,
        IonList,
        IonListHeader,
        IonLabel,
        IonItem
    }
}
</script>

<style>

</style>
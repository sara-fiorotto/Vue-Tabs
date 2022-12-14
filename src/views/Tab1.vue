<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Meu Perfil</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>

      <img id="foto_de_perfil" :src="user.imagem" />

      <h3 id="nome_de_usuario">{{ user.nome }}</h3>

      <p id="bio_de_usuario">{{ user.bio }}</p>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";

import { ref } from "vue";

import axios from "axios";

export default {
  name: "Perfil",
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  setup() {
    const user = ref({
      imagem: ``,
      nome: ``,
      bio: ``,
    });

    axios.get("https://banco-64165-default-rtdb.firebaseio.com/user/.json")
    .then(({data}) => {
      user.value = data;
    });

    return {
      user,
    };
  },
};
</script>

<style scoped>
ion-content {
  text-align: center;
}

#foto_de_perfil {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  margin: 3em auto;
  filter: invert() hue-rotate(90deg) drop-shadow(0px 0px 40px purple);
}

#nome_de_usuario {
  color: darkred;
}

#bio_de_usuario {
  width: 250px;
  margin: 3em auto;
}
</style>
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Editar Perfil</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Editar Perfil</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-list>
        <ion-item>
          <ion-label position="floating">Imagem de Perfil</ion-label>
          <ion-input @IonInput="user.imagem = $event.target.value"></ion-input>
        </ion-item>

        <ion-item>
          <ion-label position="floating">Nome de Usuario</ion-label>
          <ion-input @IonInput="user.nome = $event.target.value"></ion-input>
        </ion-item>

        <ion-item>
          <ion-label position="floating">Biografia</ion-label>
          <ion-textarea
            area-grow="true"
            @IonInput="user.bio = $event.target.value"
          ></ion-textarea>
        </ion-item>
      </ion-list>
    </ion-content>
    <ion-footer>
      <ion-button expand="full" @click="saveData">Salvar</ion-button>
    </ion-footer>
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
  name: "Tab3",
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },

  setup() {
    const user = ref({
      imagem: "",
      nome: "",
      bio: "",
    });

    function saveData() {
      axios.put(`https://banco-64165-default-rtdb.firebaseio.com/.json`, {
        user: {
          ...user.value,
        },
      });
    }

    return {
      user,
      saveData,
    };
  },
};
</script>
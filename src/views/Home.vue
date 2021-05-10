<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar color="success">
        <ion-title><b>Whatsapp Direct Message</b></ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <ion-item>
          <ion-icon :icon="call" slot="start"></ion-icon>
          <ion-label position="floating">Enter Phone Number</ion-label>
          <ion-input v-model="phoneNumber" />
        </ion-item>
        <br />
        <ion-item>
          <ion-icon slot="start" :icon="chatboxes"></ion-icon>
          <ion-label position="floating">Enter Message</ion-label>
          <ion-textarea v-model="message" />
        </ion-item>
        <br />
        <ion-button color="success" @click="sendMessage">
          <ion-icon :icon="send"></ion-icon>
          &nbsp; Send
        </ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { Plugins } from '@capacitor/core';
const { App } = Plugins;
import { send, call, chatboxes } from "ionicons/icons";
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonItem,
  IonLabel,
  IonInput,
  IonTextarea,
  IonButton,
  IonIcon,
  useBackButton,
  useIonRouter
} from "@ionic/vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "Home",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonItem,
    IonLabel,
    IonInput,
    IonTextarea,
    IonButton,
    IonIcon,
  },
  setup() {
    const ionRouter = useIonRouter();
    useBackButton(-1, () => {
      if (!ionRouter.canGoBack()) {
        App.exitApp();
      }
    });
  },
  data() {
    return {
      phoneNumber: "",
      message: "",
      send,
      call,
      chatboxes,
    };
  },
  methods: {
    sendMessage() {
      const url = `https://wa.me/+91${this.phoneNumber}?text=${this.message}`;
      window.location.href = url;
      this.phoneNumber="";
      this.message="";
    },
  },
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
</style>

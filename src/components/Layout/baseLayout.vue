<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button />
        </ion-buttons>

        <ion-title>{{ headerTitle }}</ion-title>
        <ion-buttons slot="end" v-if="route.name != 'Image'">
          <ion-button @click="$router.push({ name: 'Image' })"> Image </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>

    <ion-content
      :fullscreen="true"
      class="ion-padding-start ion-padding-vertical"
      :scroll-events="true"
    >
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">{{ headerTitle }}</ion-title>
        </ion-toolbar>
      </ion-header>

      <slot />
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonButtons,
  IonButton,
  IonBackButton,
} from "@ionic/vue";
import { defineComponent } from "vue";
import { useRoute } from "vue-router";

export default defineComponent({
  name: "Home",
  props: ["headerTitle"],
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButtons,
    IonButton,
    IonBackButton,
  },

  setup() {
    const route = useRoute();

    return { route };
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

.custom-position {
  position: absolute;
}

.text-center {
  text-align: center;
}
</style>

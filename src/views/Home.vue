<template>
  <base-layout header-title="Login Page">
    <accordion-001 :list="list">
      <template v-slot="sp">
        <ion-item>
          <div>{{ sp.item.id }} {{ sp.item.name }}</div>
          <div class="ion-text-wrap">{{ sp.item.body }}</div>
        </ion-item>

        <ion-button
          class="ion-float-right"
          style="zoom: 0.9"
          v-on:click="buttonClicked(sp.item)"
        >
          Detail
        </ion-button>
      </template>
    </accordion-001>
  </base-layout>
</template>

<script lang="ts">
import Accordion001 from "@/components/Accordion/accordion001.vue";
import { IonItem, IonButton } from "@ionic/vue";
import { defineComponent } from "vue";

interface ContentData {
  id?: number;
  name?: string;
  body?: string;
}

export default defineComponent({
  name: "Home",
  components: { Accordion001, IonItem, IonButton },

  setup() {
    const list: Array<ContentData> = [
      { id: 1, name: "aaron" },
      { id: 2, name: "andrea" },
      { id: 3, name: "bryce" },
      {
        id: 4,
        name: "reina",
        body:
          "this is some long text that should take up a bunch of space in the panel when it slides down",
      },
      {
        id: 5,
        name: "ricky",
        body:
          "this is some long text that should take up a bunch of space in the panel when it slides down" +
          " and some more really long text to this item to see what we get",
      },
      {
        id: 5,
        name: "Mile",
        body:
          "this is some long text that should take up a bunch of space in the panel when it slides down",
      },
    ];
    return {
      list,
    };
  },
});
</script>

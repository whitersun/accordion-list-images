<template>
  <div v-for="(item, i) in displayList" :key="i">
    <button class="accordion" @click="headerClicked($event)">
      <div class="custom-accordion">
        <div class="">
          {{ item.name }}
        </div>

        <div class="">
          <ion-icon icon="chevron-down-icon" />
        </div>
      </div>
    </button>

    <div class="panel">
      <slot :item="item"></slot>
    </div>
  </div>
</template>

<script lang="ts">
import { IonIcon } from "@ionic/vue";
import { reactive } from "@vue/reactivity";
export default {
  name: "Accordion",
  props: ["list"],
  components: { IonIcon },

  setup(props: any) {
    const displayList = reactive(props.list);

    const headerClicked = async (_e: any) => {
      _e.currentTarget.classList.toggle("active");

      const AllPanel = document.querySelectorAll(".panel");
      AllPanel.forEach((panel: any)  => {
        if (_e.currentTarget.nextElementSibling !== panel) {
          // panel.style.maxHeight = null;
          panel.setAttribute("style", "max-height: " + null);
        }

        panel.previousElementSibling.classList.remove("active");
      });

      const panel = await _e.currentTarget.nextElementSibling;
      if (panel.style.maxHeight) {
        // panel.style.maxHeight = null
        await panel.setAttribute("style", "max-height: " + null);
      } else {
        // panel.style.maxHeight = panel.scrollHeight + 'px'
        await panel.setAttribute("style", "max-height: " + panel.scrollHeight + "px");
      }
    };

    return {
      displayList,
      headerClicked,
    };
  },
};
</script>

<style lang="scss" scoped>
.custom-accordion {
  display: flex;
  flex-flow: row;
  justify-content: space-between;
}

.accordion {
  background-color: #eee;
  color: #444;
  cursor: pointer;
  padding: 18px;
  margin: 2px;
  width: 100%;
  text-align: left;
  border: none;
  outline: none;
  transition: all 0.5s ease;
}

/* Add a background color to the button if it is clicked on (add the .active class with JS), and when you move the mouse over it (hover) */
.active,
.accordion:hover {
  background-color: #ccc;
}
/* Style the accordion panel. Note: hidden by default */
.panel {
  padding: 0 18px;
  background-color: white;
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.2s ease-out;
}
</style>

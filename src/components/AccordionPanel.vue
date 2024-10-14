<script setup lang="ts">
import { ref } from 'vue';

type AccordionPanelProps = {
  title: string;
  ariaTitle: string;
}

defineProps<AccordionPanelProps>();

const showPanel = ref(true);

const togglePanel = () => {
  showPanel.value = !showPanel.value;
}
</script>

<template>
  <div class="panel">
    <button
        :aria-controls="'accordion-content-' + ariaTitle"
        :id="'accordion-control-' + ariaTitle"
        @click.prevent="togglePanel"
        class="panel__button">
      {{ title }}

      <img src="@/assets/icons/arrow-up.png" alt="navigation-menu" v-if="showPanel"/>
      <img src="@/assets/icons/arrow-up.png" alt="navigation-menu" class="rotate-180" v-else/>
    </button>
    <div
        :aria-hidden="!showPanel"
        :id="'content-' + ariaTitle"
        class="panel__content"
        v-if="showPanel">
      <slot></slot>
    </div>
  </div>
</template>

<style scoped lang="scss">
.panel {
  border: 0.3px solid #d2d7df;
  border-radius: 8px;
  padding: 15px;
  background-color: #FFFFFF;

  &__content {
    padding: 10px 0 0 0 ;
  }

  &__button {
    padding: 0;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    background: none;
    border: none;
    cursor: pointer;

    color: #003366;
    font-size: 20px;
    line-height: 28px;
    font-weight: 700;
  }
}
</style>

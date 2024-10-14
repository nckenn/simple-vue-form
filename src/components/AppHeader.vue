<script setup lang="ts">

import Branding from "@/components/Branding.vue";
import UserProfile from "@/components/UserProfile.vue";
</script>

<template>
  <header class="header">
    <div class="header__container">
      <div class="header__container--left">
        <img src="@/assets/icons/navigation-menu.png" alt="navigation-menu" class="header__icon" />
        <Branding />
      </div>
      <div class="header__container--right">
        <img src="@/assets/icons/search.png" alt="navigation-menu" class="header__icon" />
        <UserProfile />
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
  .header {
    display: flex;
    position: sticky;
    top: 0;
    align-items: center;
    border-bottom: 1px solid #f2f2f3;
    background-color: #ffffff;

    &__container {
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 55px;
      width: 100%;
      padding-left: 20px;
      padding-right: 20px;
      gap: 20px;

      &--left {
        display: flex;
        align-items: center;
        gap: 20px;
      }

      &--right {
        display: flex;
        align-items: center;
        gap: 20px;
      }
    }

    &__icon {
      height: 20px;
      width: 20px;
      cursor: pointer;
    }

  }
</style>

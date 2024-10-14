<script setup lang="ts">
import AppHeader from "@/components/AppHeader.vue";
import ProfileDetailsPage from "@/pages/ProfileDetailsPage.vue";
</script>

<template>
  <div class="main">
    <AppHeader />
    <main class="main__content">
      <div class="main__content-wrapper">
        <ProfileDetailsPage />
      </div>
    </main>
  </div>
</template>


<script setup lang="ts">

</script>

<template>
<aside class="sidebar">
  <nav class="sidebar__navigation">
    <a href="/" class="sidebar__navigation-link sidebar__navigation-link--active">
      <img src="@/assets/icons/firm-details.png" alt="firm-details" class="sidebar__navigation-icon" />
      <span class="sidebar__navigation-dot" />
    </a>
    <a href="/" class="sidebar__navigation-link">
      <img src="@/assets/icons/permission.png" alt="permission" class="sidebar__navigation-icon" />
      <span class="sidebar__navigation-dot" />
    </a>
  </nav>
</aside>
</template>

<style scoped lang="scss">
.sidebar {
  width: 60px;
  background: #ffffff;
  z-index: 1;
  border-right: 1px solid #f2f2f3;

  &__navigation {
    display: flex;
    padding: 40px 10px 10px 10px;
    flex-direction: column;
    gap: 1rem;
    align-items: center;

    &-link {
      position: relative;
      text-decoration: none;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 35px;
      width: 35px;

      &--active {
        background: #F2F4F7;
        border-radius: 100px;
      }
    }

    &-icon {
      width: 18px;
      height: 18px;
    }

    &-dot {
      position: absolute;
      top: 0;
      right: 0;
      background: #F5A300;
      height: 8px;
      width: 8px;
      border-radius: 100px;
    }
  }
}
</style>

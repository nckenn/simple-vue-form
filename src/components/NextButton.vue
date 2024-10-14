<script setup lang="ts">

</script>

<template>
  <button type="button" class="next-button" >
    Next
    <img src="@/assets/icons/arrow-right.png" alt="navigation-menu" class="next-button__icon" />
  </button>
</template>

<style scoped lang="scss">
.next-button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  padding: 12px 20px;
  border: none;
  border-radius: 100px;
  background: #003366;
  height: 44px;
  cursor: pointer;

  color: #ffffff;
  font-size: 16px;
  font-weight: 600;
  line-height: 20.8px;

  &__icon {
    height: 24px;
    width: 24px;
  }

  &:disabled {
    background: #CED2DA;
  }
}
</style>

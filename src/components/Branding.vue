<template>
  <a href="/" class="logo">
    <img src="@/assets/icons/logo.png" alt="logo" class="logo__image" />
    Company Logo
  </a>
</template>

<style scoped lang="scss">
.logo {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 20px;
  font-weight: 800;
  text-decoration: none;
  line-height: 26px;
  letter-spacing: -0.02em;
  text-align: left;
  color: #000000;

  &o__image {
    width: 22px;
    height: 22px;
  }
}
</style>

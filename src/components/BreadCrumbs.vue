<script setup lang="ts">

</script>

<template>
  <nav class="breadcrumb">
    <ul class="breadcrumb__list">
      <li class="breadcrumb__item">
        <a href="#" class="breadcrumb__link breadcrumb__link--home">
          <img src="@/assets/icons/home.png" alt="Home" class="breadcrumb__icon" />
        </a>
      </li>
      <li class="breadcrumb__item breadcrumb__item--separator">
        <img src="@/assets/icons/chevron-right.png" alt="arrow-right" />
      </li>
      <li class="breadcrumb__item">
        <a href="#" class="breadcrumb__link">Profile</a>
      </li>
      <li class="breadcrumb__item breadcrumb__item--separator">
        <img src="@/assets/icons/slash.png" alt="slash" />
      </li>
      <li class="breadcrumb__item">
        <span class="breadcrumb__current">Profile Details</span>
      </li>
    </ul>
  </nav>
</template>

<style scoped lang="scss">
.breadcrumb {
  display: flex;
  align-items: center;
  font-size: 14px;
}

.breadcrumb__list {
  list-style: none;
  display: flex;
  align-items: center;
  padding: 0;
  margin: 0;
}

.breadcrumb__item {
  display: flex;
  align-items: center;
}

.breadcrumb__link {
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  line-height: 17.5px;
  color: #414E62;
}

.breadcrumb__link--home {
  display: flex;
}

.breadcrumb__icon {
  width: 24px;
  height: 24px;
}

.breadcrumb__item--separator {
  margin: 0 5px;
  color: #97A1AF;
}

.breadcrumb__current {
  font-size: 14px;
  font-weight: 600;
  line-height: 17.5px;
  color: #000000;
}
</style>

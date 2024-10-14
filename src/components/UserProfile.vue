<template>
  <div class="profile">
    <img src="@/assets/avatar.png" alt="avatar" class="profile__avatar" />
    <div class="profile__content">
      <span class="profile__name">Forename Surname</span>
      <span class="profile__position">Position</span>
    </div>
  </div>
</template>

<style scoped lang="scss">
.profile {
  display: flex;
  align-items: center;
  gap: 8px;

  &__avatar {
    width: 32px;
    height: 32px;
    border-radius: 300px;
  }

  &__content {
    display: flex;
    align-items: start;
    justify-content: center;
    flex-direction: column;
  }

  &__name {
    font-weight: 600;
    font-size: 14px;
    line-height: 17.5px;
  }

  &__position {
    font-weight: 400;
    font-size: 12px;
    line-height: 16px;
  }
}
</style>

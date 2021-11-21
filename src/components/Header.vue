<template>
  <header class="header">
    <div class="brand">Blintz</div>
    <div class="user">
      <span>Bem vindo, </span>
      <span class="user__email"><strong>usuario@gmail.com</strong></span>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  font-size: 1.6rem;
  height: var(--header-heigth);
  padding: 10px;
  background-color: #fff;
  box-shadow: var(--box-shadow-0);
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 10;

  display: flex;
  justify-content: space-around;
  align-items: center;
}

.brand {
    font-size: 2.6rem;
    font-weight: 700;
}

.header .user {
    color: var(--color-2);
}
</style>
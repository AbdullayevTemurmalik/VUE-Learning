<script setup>
const props = defineProps({
  likes: Number,
  cartCount: Number,
});

const emit = defineEmits(["toggle-cart"]);
</script>

<template>
  <nav class="navbar">
    <h1 class="logo">Moon Shop</h1>
    <div class="nav-icons">
      <span class="like-count">❤️ {{ likes }}</span>
      <span class="cart-icon" @click="emit('toggle-cart')">
        🛒 {{ cartCount }}
      </span>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #212529;
  color: #fff;
  padding: 15px 40px;
}
.logo {
  font-size: 24px;
}
.nav-icons {
  display: flex;
  gap: 20px;
  font-size: 20px;
  cursor: pointer;
}
</style>

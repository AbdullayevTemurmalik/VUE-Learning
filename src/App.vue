<script setup>
import { ref, computed } from "vue";
import Navbar from "./components/Navbar.vue";

const products = ref([
  {
    id: 1,
    name: "Smart Watch",
    price: 120,
    img: "https://images.unsplash.com/photo-1519744792095-2f2205e87b6f",
    liked: false,
  },
  {
    id: 2,
    name: "Headphones",
    price: 80,
    img: "https://images.unsplash.com/photo-1517336714731-489689fd1ca8",
    liked: false,
  },
  {
    id: 3,
    name: "Smartphone",
    price: 699,
    img: "https://images.unsplash.com/photo-1511707171634-5f897ff02aa9",
    liked: false,
  },
  {
    id: 4,
    name: "Laptop",
    price: 999,
    img: "https://images.unsplash.com/photo-1517336714731-489689fd1ca8",
    liked: false,
  },
]);

const cart = ref([]);
const showCart = ref(false);

const toggleLike = (product) => {
  product.liked = !product.liked;
};

const addToCart = (product) => {
  cart.value.push(product);
  showCart.value = true;
};

const closeCart = () => {
  showCart.value = false;
};

const totalPrice = computed(() =>
  cart.value.reduce((sum, item) => sum + item.price, 0)
);
</script>

<template>
  <div class="app">
    <!-- Navbar -->
    <Navbar
      :likes="products.filter((p) => p.liked).length"
      :cart-count="cart.length"
      @toggle-cart="showCart = !showCart"
    />

    <div class="product-list">
      <div class="card" v-for="product in products" :key="product.id">
        <img :src="product.img" alt="product" />
        <h2>{{ product.name }}</h2>
        <p>${{ product.price }}</p>
        <div class="buttons">
          <button
            class="like-btn"
            :class="{ active: product.liked }"
            @click="toggleLike(product)"
          >
            ❤️
          </button>
          <button class="add-btn" @click="addToCart(product)">
            Add to Cart
          </button>
        </div>
      </div>
    </div>

    <div class="modal" v-if="showCart">
      <div class="modal-content">
        <h2>🛒 Your Cart</h2>
        <div v-if="cart.length === 0" class="empty">Cart is empty</div>
        <div v-else>
          <div class="cart-item" v-for="(item, index) in cart" :key="index">
            <img :src="item.img" alt="cart item" />
            <div class="info">
              <p>{{ item.name }}</p>
              <span>${{ item.price }}</span>
            </div>
          </div>
          <h3>Total: ${{ totalPrice }}</h3>
        </div>
        <button class="close-btn" @click="closeCart">Close</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app {
  font-family: "Poppins", sans-serif;
  background: #f8f9fa;
  min-height: 100vh;
}

/* Products grid */
.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
  gap: 25px;
  padding: 40px;
}

.card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 15px;
  text-align: center;
  transition: 0.3s;
}
.card:hover {
  transform: translateY(-5px);
}
.card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-radius: 8px;
}
.card h2 {
  margin: 10px 0;
  font-size: 18px;
}
.card p {
  color: #555;
  margin-bottom: 10px;
}
.buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
}
.like-btn,
.add-btn {
  border: none;
  cursor: pointer;
  padding: 8px 14px;
  border-radius: 8px;
  font-size: 14px;
  transition: 0.3s;
}
.like-btn {
  background: #ffe3e3;
}
.like-btn.active {
  background: #ff6b6b;
  color: white;
}
.add-btn {
  background: #0d6efd;
  color: white;
}
.add-btn:hover {
  background: #0b5ed7;
}

/* Modal */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-content {
  background: #fff;
  border-radius: 12px;
  padding: 20px;
  width: 400px;
  max-height: 80vh;
  overflow-y: auto;
}
.cart-item {
  display: flex;
  align-items: center;
  gap: 15px;
  margin: 10px 0;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
}
.cart-item img {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: 8px;
}
.info p {
  margin: 0;
  font-weight: 500;
}
.close-btn {
  background: #dc3545;
  border: none;
  color: white;
  padding: 10px 16px;
  border-radius: 8px;
  cursor: pointer;
  margin-top: 15px;
}
.close-btn:hover {
  background: #bb2d3b;
}
.empty {
  text-align: center;
  padding: 20px;
  color: #888;
}
</style>

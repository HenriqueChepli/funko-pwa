<script setup>
import { ref, onMounted } from 'vue'
import $ from 'jquery'
import 'slick-carousel/slick/slick.css'
import 'slick-carousel/slick/slick-theme.css'
import 'slick-carousel'

import akiIMG from './assets/img/aki.png';
import denjiIMG from './assets/img/denji.png';
import dexterIMG from './assets/img/dexter.png';
import freddieMercuryIMG from './assets/img/freedie mercury.png';
import ichigoIMG from './assets/img/ichigo.png';
import ironmanIMG from './assets/img/ironmark.png';
import louisIMG from './assets/img/louis.png';
import spidermanIMG from './assets/img/spiderman.png';
import thanosIMG from './assets/img/thanos.png';
import michaelJacksonIMG from './assets/img/michael.png';

onMounted(() => {
  $('.slick-carousel').slick({
    slidesToShow: 5,
    slidesToScroll: 1,
    arrows: true,
    dots: true,
    infinite: true,
    responsive: [
      {
        breakpoint: 1024,
        settings: {
          slidesToShow: 3,
        }
      },
      {
        breakpoint: 768,
        settings: {
          slidesToShow: 2,
        }
      },
      {
        breakpoint: 480,
        settings: {
          slidesToShow: 1,
        }
      }
    ]
  })
})

const cart = ref(0)
const cartItems = ref([])
const showCart = ref(false)

const increaseQuantity = () => {
  if (cart.value < Funko.value.inStock) {
    cart.value += 1
  } else {
    alert("Produto fora de estoque!")
  }
}

const decreaseQuantity = () => {
  if (cart.value > 0) {
    cart.value -= 1
  }
}

const buyProduct = () => {
  if (cart.value > 0) {
    Funko.value.inStock -= cart.value
    const existingItem = cartItems.value.find(item => item.id === Funko.value.id)
    if (existingItem) {
      existingItem.quantity += cart.value
    } else {
      cartItems.value.push({
        id: Funko.value.id,
        name: Funko.value.name,
        price: Funko.value.price,
        quantity: cart.value,
        image: Funko.value.image,
      })
    }
    alert(`Você adicionou ${cart.value} unidade(s) de ${Funko.value.name} ao carrinho!`)
    cart.value = 0
  } else {
    alert("Seu carrinho está vazio!")
  }
}

const toggleCart = () => {
  showCart.value = !showCart.value
}

const totalPrice = (price, quantity) => {
  return (parseFloat(price.replace(",", ".")) * quantity).toFixed(2).replace(".", ",")
}

const changeImage = (selectedFunko) => {
  Funko.value = selectedFunko
}

const funkos = [
  { id: 1, name: "Aki", image: akiIMG, price: "49,99", installment: "10,00", description: "Aki de Chainsaw Man...", inStock: 5 },
  { id: 2, name: "Denji", image: denjiIMG, price: "229,99", installment: "46,00", description: "Denji de Chainsaw Man...", inStock: 5 },
  { id: 3, name: "Dexter", image: dexterIMG, price: "89,99", installment: "18,00", description: "Dexter, o cientista mirim...", inStock: 5 },
  { id: 4, name: "Freddie Mercury", image: freddieMercuryIMG, price: "119,99", installment: "24,00", description: "Freddie Mercury, o lendário cantor...", inStock: 5 },
  { id: 5, name: "Ichigo", image: ichigoIMG, price: "109,99", installment: "22,00", description: "Ichigo Kurosaki de Bleach...", inStock: 5 },
  { id: 6, name: "Ironman", image: ironmanIMG, price: "199,99", installment: "40,00", description: "Iron Man da Marvel...", inStock: 5 },
  { id: 7, name: "Louis", image: louisIMG, price: "89,99", installment: "18,00", description: "Louis de Entourage...", inStock: 5 },
  { id: 8, name: "Spiderman", image: spidermanIMG, price: "149,99", installment: "30,00", description: "Spider-Man, o herói da Marvel...", inStock: 5 },
  { id: 9, name: "Thanos", image: thanosIMG, price: "169,99", installment: "34,00", description: "Thanos, o vilão da Marvel...", inStock: 5 },
  { id: 10, name: "Michael Jackson", image: michaelJacksonIMG, price: "599,99", installment: "120,00", description: "Michael Jackson, o Rei do Pop...", inStock: 5 },
]

const Funko = ref(funkos[0])
</script>

<template>
  <header>
    <nav>
      <div class="nav-logo">
        <img src="./assets/img/funko-seeklogo.png" alt="Funko Logo" />
      </div>
      <div class="nav-cart" @click="toggleCart">
        <img src="./assets/img/carrinho.png" alt="Carrinho" />
      </div>
    </nav>
  </header>

  <div class="banner-container">
    <img src="./assets/img/image (1).png" alt="Banner" class="banner-image" />
  </div>

  <!-- CARROSSEL -->
  <div class="funko-carousel">
    <div class="slick-carousel">
      <div v-for="funko in funkos" :key="funko.id" class="slide" @click="changeImage(funko)">
        <img :src="funko.image" :alt="funko.name" />
      </div>
    </div>
  </div>

  <main>
    <div class="main">
      <div class="img">
        <img :src="Funko.image" alt="Selected Funko" />
      </div>
      <div class="info">
        <h1>{{ Funko.name }}</h1>
        <p>{{ Funko.description }}</p>
        <p class="price">R${{ Funko.price }}</p>
        <p class="installment">Ou por R${{ Funko.installment }} em 5x sem juros</p>
        <p>Estoque: {{ Funko.inStock }} unidades</p>
        <p>Quantidade no carrinho: {{ cart }}</p>
        <p class="price" v-if="cart > 0">Total: R${{ totalPrice(Funko.price, cart) }}</p>
        <p class="installment" v-if="cart > 0">Total em 5x: R${{ totalPrice(Funko.installment, cart) }}</p>
        <div class="quantity-selector">
          <button :disabled="Funko.inStock < 1" @click="decreaseQuantity">-</button>
          <p>{{ cart }}</p>
          <button :disabled="Funko.inStock < 1" @click="increaseQuantity">+</button>
        </div>
        <button class="buy-button" @click="buyProduct">Comprar</button>
      </div>
    </div>
  </main>

  <footer>
    <img src="./assets/img/funko-seeklogo.png" alt="Logo Footer" />
    <h2>Contate-nos!</h2>
    <p>&copy; 2025 Funko Store. Todos os direitos reservados.</p>
  </footer>

  <div v-if="showCart" class="cart-sidebar">
    <div class="cart-header">
      <h2>Suas Compras</h2>
      <button @click="toggleCart" class="close-cart">Fechar</button>
    </div>
    <div v-if="cartItems.length > 0" class="cart-content">
      <div v-for="item in cartItems" :key="item.id" class="cart-item">
        <img :src="item.image" :alt="item.name" class="cart-item-image" />
        <div class="cart-item-info">
          <h3>{{ item.name }}</h3>
          <p>Preço: R${{ item.price }}</p>
          <p>Quantidade: {{ item.quantity }}</p>
          <p>Total: R${{ totalPrice(item.price, item.quantity) }}</p>
        </div>
      </div>
    </div>
    <div v-else class="empty-cart">
      <p>Você ainda não comprou nada!</p>
    </div>
  </div>
</template>

<style scoped>
.slick-carousel {
  margin: 20px auto;
  width: 90%;
}
.slide img {
  width: 100%;
  max-height: 200px;
  object-fit: contain;
  padding: 10px;
  border-radius: 12px;
  cursor: pointer;
}
.quantity-selector button {
  padding: 0 10px;
}
</style>

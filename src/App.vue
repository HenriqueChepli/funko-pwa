<script setup>
import { ref } from 'vue';
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

 const cart = ref(0);
    const cartItems = ref([]);
    const showCart = ref(false);

    const increaseQuantity = () => {
      if (cart.value < Funko.value.inStock) {
        cart.value += 1;
      } else {
        alert("Produto fora de estoque!");
      }
    };

    const decreaseQuantity = () => {
      if (cart.value > 0) {
        cart.value -= 1;
      }
    };

    const buyProduct = () => {
      if (cart.value > 0) {
        // Atualizar o estoque
        Funko.value.inStock -= cart.value;

        // Verificar se o item já está no carrinho
        const existingItem = cartItems.value.find(item => item.id === Funko.value.id);
        if (existingItem) {
          existingItem.quantity += cart.value;
        } else {
          cartItems.value.push({
            id: Funko.value.id,
            name: Funko.value.name,
            price: Funko.value.price,
            quantity: cart.value,
            image: Funko.value.image,
          });
        }

        alert(`Você adicionou ${cart.value} unidade(s) de ${Funko.value.name} ao carrinho!`);
        cart.value = 0;
      } else {
        alert("Seu carrinho está vazio!");
      }
    };

    const toggleCart = () => {
      showCart.value = !showCart.value; // Alterna entre abrir e fechar o carrinho
    };

    const totalPrice = (price, quantity) => {
      return (parseFloat(price.replace(",", ".")) * quantity).toFixed(2).replace(".", ",");
    };

    const changeImage = (selectedFunko) => {
      Funko.value = selectedFunko;
    };


    const funkos = [
      {
        id: 1,
        name: "Aki",
        image: akiIMG,
        price: (49.99).toFixed(2).replace(".", ","),
        installment: (49.99 / 5).toFixed(2).replace(".", ","),
        description:
          "Aki de Chainsaw Man, com seu visual icônico e expressão de determinação. Ele é um personagem forte, de personalidade séria, mas com um coração bondoso. Seu estilo combina com sua natureza corajosa e obstinada.",
        inStock: 5,
      },
      {
        id: 2,
        name: "Denji",
        image:  denjiIMG,
        price: (229.99).toFixed(2).replace(".", ","),
        installment: (229.99 / 5).toFixed(2).replace(".", ","),
        description:
          "Denji de Chainsaw Man, com a motosserra e seu estilo irreverente. Denji é um jovem sonhador, tentando levar uma vida melhor, enquanto combate demônios com seu poder transformador. Um Funko que captura sua personalidade ousada e destemida.",
        inStock: 5,
      },
      {
        id: 3,
        name: "Dexter",
        image: dexterIMG,
        price: (89.99).toFixed(2).replace(".", ","),
        installment: (89.99 / 5).toFixed(2).replace(".", ","),
        description:
          "Dexter, o cientista mirim de Dexter's Laboratory, com seu traje clássico de laboratório. Com sua inteligência fora do comum, Dexter adora inventar, mas também acaba se metendo em muitas confusões devido à sua atitude impulsiva.",
        inStock: 5,
      },
      {
        id: 4,
        name: "Freddie Mercury",
        image: freddieMercuryIMG,
        price: (119.99).toFixed(2).replace(".", ","),
        installment: (119.99 / 5).toFixed(2).replace(".", ","),
        description:
          "Freddie Mercury, o lendário cantor do Queen, com sua pose característica. Ele é lembrado como um dos maiores vocalistas da história do rock, e essa figura captura sua energia única no palco e seu estilo inconfundível.",
        inStock: 5,
      },
      {
        id: 5,
        name: "Ichigo",
        image: ichigoIMG,
        price: (109.99).toFixed(2).replace(".", ","),
        installment: (109.99 / 5).toFixed(2).replace(".", ","),
        description:
          "Ichigo Kurosaki de Bleach, com sua espada e expressão decidida. Ichigo é um dos maiores heróis dos animes, com uma história de sacrifício e luta contra forças sobrenaturais, e esse Funko reflete sua coragem e determinação.",
        inStock: 5,
      },
      {
        id: 6,
        name: "Ironman",
        image: ironmanIMG,
        price: (199.99).toFixed(2).replace(".", ","),
        installment: (199.99 / 5).toFixed(2).replace(".", ","),
        description:
          "Iron Man (Homem de Ferro), o herói da Marvel com sua armadura vermelha brilhante. Tony Stark, o gênio milionário, torna-se o icônico Iron Man após desenvolver uma armadura poderosa, e esse Funko reflete sua tecnologia avançada e coragem.",
        inStock: 5,
      },
      {
        id: 7,
        name: "Louis",
        image: louisIMG,
        price: (89.99).toFixed(2).replace(".", ","),
        installment: (89.99 / 5).toFixed(2).replace(".", ","),
        description:
          'Louis de Entourage, sempre com sua atitude descontraída e estilo único. Louis é o empresário que gerencia a carreira de seu amigo Vince, sempre preocupado com o sucesso dos outros e mantendo seu charme e estilo inconfundíveis.',
        inStock: 5,
      },
      {
        id: 8,
        name: "Spiderman",
        image: spidermanIMG,
        price: (149.99).toFixed(2).replace(".", ","),
        installment: (149.99 / 5).toFixed(2).replace(".", ","),
        description:
          "Spider-Man (Homem-Aranha), o herói da Marvel com sua famosa máscara e traje vermelho e azul. Peter Parker usa seus poderes para proteger Nova York e essa figura captura seu equilíbrio entre ser um herói e enfrentar a vida cotidiana.",
        inStock: 5,
      },
      {
        id: 9,
        name: "Thanos",
        image: thanosIMG,
        price: (169.99).toFixed(2).replace(".", ","),
        installment: (169.99 / 5).toFixed(2).replace(".", ","),
        description:
          "Thanos, o vilão intergaláctico de Marvel, com a Manopla do Infinito. Sua missão de destruir metade da vida no universo com um estalar de dedos tornou-se uma das maiores histórias da cultura pop, e seu Funko captura a gravidade de sua presença.",
        inStock: 5,
      },
      {
        id: 10,
        name: "Michael Jackson",
        image: michaelJacksonIMG,
        price: (599.99).toFixed(2).replace(".", ","),
        installment: (599.99 / 5).toFixed(2).replace(".", ","),
        description: "Michael Jackson, o Rei do Pop, capturado em uma pose clássica com seu famoso casaco. Conhecido por sua música revolucionária e estilo único, Michael Jackson é uma lenda que continua a influenciar a música e a cultura.",
        inStock: 5,
      },
    ];

    const Funko = ref(funkos[0]);
</script>

<template>
      <header>
        <nav>
          <div class="nav-logo">
            <img src="./assets/img/funko-seeklogo.png" alt="Funko Logo">
          </div>
          <div class="nav-cart" @click="toggleCart">
            <img src="./assets/img/carrinho.png" alt="Carrinho">
          </div>
        </nav>
      </header>
  
      <div class="banner-container">
        <img src="./assets/img/image (1).png" alt="Banner" class="banner-image">
      </div>
  
      <div class="funkos">
        <ul class="carousel">
          <li v-for="funko in funkos" :key="funko.id">
            <img :src="funko.image" @mouseover="changeImage(funko)" :alt="funko.name">
  
          </li>
        </ul>
      </div>
  
      <main>
        <div class="main">
          <div class="img">
            <img :src="Funko.image" alt="Selected Funko">
          </div>
          <div class="info">
            <h1>{{ Funko.name }}</h1>
            <p>{{ Funko.description }}</p>
            <p class="price">R${{ Funko.price }}</p>
            <p class="installment">Ou por R${{Funko.installment}} em 5x sem juros</p>
            <p>Estoque: {{ Funko.inStock }} unidades</p>
            <p>Quantidade no carrinho: {{ cart }}</p>
            <p class="price" v-if="cart > 0">Total: R${{ totalPrice(Funko.price, cart) }}</p>
            <p class="installment" v-if="cart > 0">Total em 5x: R${{ totalPrice(Funko.installment, cart) }}</p>
            <div class="quantity-selector">
              <button :class="{disableButton: Funko.inStock < 1}" :disabled="Funko.inStock < 1" @click="decreaseQuantity">-</button>
              <p>{{ cart }}</p>
              <button :class="{disableButton: Funko.inStock < 1}" :disabled="Funko.inStock < 1" @click="increaseQuantity">+</button>
            </div>
            <button class="buy-button" @click="buyProduct">Comprar</button>
          </div>
        </div>
      </main>
      <footer>
        <img src="./assets/img/funko-seeklogo.png" alt="Logo Footer">
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
            <img :src="item.image" :alt="item.name" class="cart-item-image">
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
</style>

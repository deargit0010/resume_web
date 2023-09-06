<!-- <template>
  <div class="section" data-theme="dracula">
    <div class="flex h-screen">
      <div class="m-auto">
        <h3 class="text-9xl">Kittithat Auaiphon</h3>
        <div class="mockup-window border bg-base-300">
          <div class="px-4 py-16 bg-base-200">

            <div class="chat chat-start">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/itachi.png"/>
                </div>
              </div>
              <div class="chat-header">Interview Committee</div>
              <div class="chat-bubble chat-bubble-secondary">
                tell me about your history
              </div>
            </div>
            <div class="chat chat-end">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/ME.jpg"/>
                </div>
              </div>
              <div class="chat-header">Kittithat Auaiphon</div>
              <div class="chat-bubble chat-bubble-success">
                My name : Kittithat Auaiphon
              </div>
            </div>
            <div class="chat chat-end">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/ME.jpg"/>
                </div>
              </div>
              <div class="chat-header">Kittithat Auaiphon</div>
              <div class="chat-bubble chat-bubble-success">Age : 21 years</div>
            </div>
            <div class="chat chat-end">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/ME.jpg"/>
                </div>
              </div>
              <div class="chat-header">Kittithat Auaiphon</div>
                <div class="chat-bubble chat-bubble-success">graduated primary school from Wat Phraya Pla School.</div>
            </div>
            <div class="chat chat-end">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/ME.jpg"/>
                </div>
              </div>
              <div class="chat-header">Kittithat Auaiphon</div>
                <div class="chat-bubble chat-bubble-success">graduated high school from Nawaminthrachinuthit Suankularb Wittayalai PathumThani School</div>
            </div>
            <div class="chat chat-end">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/ME.jpg"/>
                </div>
              </div>
              <div class="chat-header">Kittithat Auaiphon</div>
                <div class="chat-bubble chat-bubble-success">Studying at Mahanakorn University of Technology</div>
            </div>
            <div class="chat chat-start">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/itachi.png"/>
                </div>
              </div>
              <div class="chat-header">Interview Committee</div>
              <div class="chat-bubble chat-bubble-secondary">What about your human relations?</div>
            </div>
            <div class="chat chat-end">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/ME.jpg"/>
                </div>
              </div>
              <div class="chat-header">Kittithat Auaiphon</div>
                <div class="chat-bubble chat-bubble-success">I'm easy to get along with.</div>
            </div>
            <div class="chat chat-start">
              <div class="chat-image avatar">
                <div class="w-10 rounded-full">
                  <img src="./assets/itachi.png"/>
                </div>
              </div>
              <div class="chat-header">Interview Committee</div>
              <div class="chat-bubble chat-bubble-secondary">OKAY.</div>
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
  
</template> -->

<!-- <template>
  <table class="table">
    <thead>
      <tr>
        <td><th>#</th></td>
        <td><th>Product</th></td>
        <td><th>price</th></td>
      </tr>
      <tr>
        <th>
          <tr><td>1</td></tr>
          <tr><td>2</td></tr>
          <tr><td>3</td></tr>
          <tr><td>4</td></tr>
          <tr><td>5</td></tr>
          <tr><td>6</td></tr>
          <tr><td>7</td></tr>
          <tr><td>8</td></tr>
          <tr><td>9</td></tr>
          <tr><td>10</td></tr>
          <tr><td>11</td></tr>
        </th>
          <td>
            <div v-for="product in products" :key="product._id">
              <tr><td>{{ product.name }}</td></tr>
            </div>
          </td>
          <td>
            <div v-for="product in products" :key="product._id">
              <tr><td>{{ product.price }}</td></tr>
            </div>
          </td>
      </tr>
      
    </thead>
  </table>
</template> -->

<!-- <script setup>
import axios from "axios";
import { ref, onMounted } from "vue";

const products = ref();
onMounted(async () => {
  products.value = await getAllProduct();
  console.log(products);
});

const getAllProduct = async () => {
  let data = [];
  await axios.get("http://localhost:5000/getallproduct").then((response) => {
    data = response.data;
  });
  return data;
};
</script>

<style scoped>
.section {
  height: 100vh;
}
</style> -->


<template>
  <header>
    <div class="navbar bg-base-100">
      <div class="navbar-start">
        <div class="dropdown">
          <label tabindex="0" class="btn btn-ghost lg:hidden">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h8m-8 6h16" /></svg>
          </label>
          <ul tabindex="0" class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52">
            <li v-for="menu in menuList" :key="menu.name"><RouterLink :to="menu.path" >{{ menu.name }}</RouterLink></li>
          </ul>
        </div>
        <a class="btn btn-ghost normal-case text-xl">daisyUI</a>
      </div>
      <div class="navbar-center hidden lg:flex">
        <ul class="menu menu-horizontal px-1">
          <li v-for="menu in menuList" :key="menu.name"><RouterLink :to="menu.path">{{ menu.name }}</RouterLink></li>
        </ul>
      </div>
      <!-- <div class="navbar-end">
        <a class="btn">Button</a>
      </div> -->
    </div>
  </header>
  <div class="container mx-auto">
    <RouterView :key="router.currentRoute.value.name"></RouterView>
  </div>
</template>

<script setup>
import { RouterView, RouterLink } from 'vue-router';
import { useRouter } from 'vue-router';
import router from './router';
const menuList = [
  { path:"/", name: "home"},
  { path:"/create", name: "create"}
]

</script>

<style scoped>

</style>

<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import { useRouter } from "vue-router";
let name = ref(''), 
    price = ref(0), 
    routerName = ref(''), 
    _id = ref('');
const router = useRouter()
onMounted(() => {
    routerName.value = router.currentRoute.value.name;
    _id.value = router.currentRoute.value.params?.id;
    console.log("routerName", routerName.value);
    console.log("_id", _id.value);
    if(routerName.value == "edit") {
        initEdit();
    }
});
const API_PATH = import.meta.env.VITE_API_PATH;
const initEdit = async () => {
    const {data} = await axios.get(`${API_PATH}/getproduct/${_id.value}`);
    name.value = data.data.name;
    price.value = data.data.price;
}
const submit = async () => {
    const req = {
        name:name.value, price:price.value
    };
    if(routerName.value == "create" ) {
        await axios.post(
            `${API_PATH}/create`,
            req
        ).then((response) => {
            name.value = '';
            price.value = '';
        });
    } else {
        await axios.post(
            `${API_PATH}/${_id.value}`,
            req
        ).then((response) => {
            router.push({name : 'home', replace: true});
        });
    }
 };
 
</script>

<!-- <script setup>
import axios from "axios";
import { ref, onMounted } from "vue";
const products = ref([]);
onMounted(async () => {
  products.value = await getAllProduct();
});
const getAllProduct = async () => {
  let data = [];
  data = await axios
    .get("http://localhost:5000/getallproduct")
    .then((response) => {
      return response.data;
    });
  return data;
};
</script> -->

<template>
    <div class="flex h-screen">
        <div class="m-auto container">
            <div class="mockup-window border border-base-300" data-theme="valentine">
                <div class="flex justify-center px-4 py-16 border-t border-base-300">
                    <table class="table text-lg">
                        <thead class="text-xl">
                                <input type="text" placeholder="Name" class="input input-bordered w-full max-w-xs" v-model="name"  />
                                <input type="number" placeholder="Price" class="input input-bordered w-full max-w-xs" v-model="price"  />
                                <button class="btn btn-warning btn-success" v-on:click = "$event => submit()">Confirm</button>
                        </thead>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
<template>
  <div class="pt-16">
    <h1 class="text-3xl font-semibold mb-4">Enter Your Phone Number</h1>
    <form action="#" @submit="handleLogin">
      <div
        class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left"
      >
        <div class="bg-white px-4 py-5 sm:p-6">
          <div>
            <input
              type="text"
              name="phone"
              v-maska
              data-maska="### (###) ###-###"
              v-model="credentials.phone"
              id="phone"
              placeholder="+254 724 071 015"
              class="mt-1 block w-full px-3 py-2 rounded-md border-gray-300"
            />
          </div>
        </div>
        <div class="bg-gray-50 px-4 py-3 text-right sm:px-6">
          <button
            type="submit"
            @submit.prevent="handleLogin"
            class="inline-flex justify-center rounded-md border border-transparent bg-black py-2"
          >
            Continue
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script setup>
import { vMaska } from "maska";
import { reactive } from "vue";
import axios from "axios";

const credentials = reactive({
  phone: null,
});

const handleLogin = () => {
axios.post("http://localhost/api/login", {
    phone: credentials.phone.replaceAll(' ', '').replace('(', '').replace(')', '').replace('-', '')
})
    .then((response) => {
      console.log(response.data);
    })
    .catch((error) => {
      console.error(error);
      alert(error.response.data.message);
    })
}
</script>

<style></style>

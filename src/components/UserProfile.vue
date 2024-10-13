<script setup>
import { ref } from "vue";
import imageUpload from "@/components/imageUpload.vue";
import { useRouter } from "vue-router";
const router = useRouter();
import { useAuthStore } from "@/stores/authstore";
const authstore = useAuthStore();
authstore.initializeAuth();
const storedUser = ref(JSON.parse(localStorage.getItem("user")));
const logoutUser = () => {
  router.push("/");
};
const fullName =
  authstore.user?.fName.charAt(0).toUpperCase() +
  authstore.user?.fName.slice(1) +
  " " +
  authstore.user?.lName.charAt(0).toUpperCase() +
  authstore.user?.lName.slice(1);
const fullRole =
  authstore.user?.role.charAt(0).toUpperCase() + authstore.user?.role.slice(1);
</script>
<template>
  <div class="bg-gray-700">
    <div class="shadow-xl rounded-xl w-fit flex justify-end items-end p-6">
      <button
        @click="logoutUser"
        class="mr-6 bg-white rounded-lg shadow-lg p-1 hover:text-blue-500"
      >
        Logout
      </button>
    </div>
    <div class="min-h-screen flex justify-center items-center p-3">
      <div
        class="py-8 px-8 max-w-xl mx-auto bg-white rounded-xl shadow-lg space-y-2 sm:py-4 sm:flex sm:items-center sm:space-y-0 sm:space-x-6 w-fit"
      >
        <imageUpload />

        <div class="text-center space-y-2 sm:text-left">
          <div class="space-y-0.5">
            <p class="text-lg text-black font-semibold">{{ fullName }}</p>
            <p class="text-slate-500 font-medium">{{ fullRole }}</p>
          </div>
        </div>
        <div></div>
      </div>
    </div>
  </div>
</template>
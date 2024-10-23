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
  authstore.loginUser
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
  <div class="bg-black min-h-screen  flex justify-center items-center">
    <div class="bg-white shadow-xl rounded-xl p-1 m-auto opacity-2 hover:text-slate-900">
      <span @click="logoutUser" class="text-slate-500 hover:text-slate-900 hover:underline">LOG OUT</span>
    </div>
    <div
      class="py-8 px-8 max-w-sm mx-auto space-y-2 bg-white rounded-xl shadow-xl sm:py-4 sm:flex sm:items-center sm:space-y-0 sm:gap-x-6 ">
      <imageUpload />
      <div class="text-center space-y-2 sm:text-left">
        <div class="space-y-0.5">
          <p class="text-lg text-black font-semibold">
            {{ fullName }}
          </p>
          <p class="text-slate-500 font-medium">
            {{ fullRole }}
          </p>
        </div>
        <button
          class="px-4 py-1 text-sm text-purple-600 font-semibold rounded-full border border-purple-200 hover:text-white hover:bg-purple-600 hover:border-transparent focus:outline-none focus:ring-2 focus:ring-purple-600 focus:ring-offset-2">Review</button>
      </div>
    </div>

  </div>


</template>
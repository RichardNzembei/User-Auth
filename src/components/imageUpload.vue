<template>
  <div class="relative w-32 h-32 mx-auto">
    <img
      :src="imageData || defaultProfileImage"
      alt="Profile Image"
      class="w-full h-full object-cover rounded-full border"
      @error="imageData = defaultProfileImage"
    />

    <label
      for="fileInput"
      class="absolute inset-0 bg-black bg-opacity-50 flex justify-center items-center rounded-full opacity-0 hover:opacity-100 transition-opacity cursor-pointer"
    >
      <i class="fas fa-camera text-white text-xl"></i>
      <input
        id="fileInput"
        type="file"
        @change="handleFileUpload"
        accept="image/*"
        class="hidden"
      />
    </label>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const defaultProfileImage = new URL(
  "../assets/img/profile-icon.png",
  import.meta.url
).href;

const imageData = ref("");

function handleFileUpload(event) {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();

    reader.onload = (e) => {
      imageData.value = e.target.result;
      localStorage.setItem("uploadedImage", imageData.value);
    };

    reader.readAsDataURL(file);
  }
}

onMounted(() => {
  const storedImage = localStorage.getItem("uploadedImage");
  if (storedImage) {
    imageData.value = storedImage;
  }
});
</script>

<style scoped>
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css");
</style>

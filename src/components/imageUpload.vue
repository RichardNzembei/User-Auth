<template>
  <div>
    <img
      v-if="imageData"
      :src="imageData"
      alt="Uploaded Image"
      class="block mx-auto h-24 rounded-full sm:mx-0 sm:shrink-0"
    />
    <input type="file" @change="handleFileUpload" accept="image/*" />
  </div>
</template>
  
  <script setup>
import { ref, onMounted } from "vue";

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
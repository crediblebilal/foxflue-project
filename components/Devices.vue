
<template>
  <div class="bg-[#fcfcfc] mb-1 text-justify pt-3">
    <p class="font-semibold text-xl relative left-0">Devices</p>
    <div class="flex justify-around m-2 border-b-2 pb-4">

      <div class="flex">
        <NuxtImg src="/ip2.jpeg" width="50px" class="mr-2 md:mr-3" />
        <div>
          <p class="font-semibold">iPhone 13 </p>
          <p class="text-gray-600">128GB - Unlocked - Good</p>
          <p class="font-semibold text-blue-500"> Estimated offer $750 </p>
        </div>
      </div>
      <div>
        <button class="p-2 bg-red-500 text-white rounded-md hover:bg-rose-700" @click="openImageCaptureDialog">Start Inspection</button>
      </div>

    </div>

    <div class="flex justify-around p-2 bg-[#fcfcfc]">

      <div class="flex">
        <NuxtImg src="/ip2.jpeg" width="50px" class="mr-2 md:mr-3" />
        <div>
          <p class="font-semibold">iPhone 13 pro max</p>
          <p class="text-gray-600">128GB - Unlocked - Flawless</p>
          <p class="font-semibold text-blue-500"> Estimated offer $550 </p>
        </div>
      </div>
      <div>
        <button class="p-2 bg-red-500 text-white rounded-md hover:bg-rose-700" @click="openImageCaptureDialog" >Start Inspection</button>
      </div>

    </div>



    <div>
      <ImageCaptureDialog v-show="showImageCaptureDialog" @close-modal="showImageCaptureDialog = false" />
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import ImageCaptureDialog from '@/components/ImageCaptureDialog.vue';

export default {
  components: {
    ImageCaptureDialog,
  },
  data() {
    return {
      showImageCaptureDialog: false,
      imageSrc: null, // This will store the captured image as a Base64 string
    };
  },
  methods: {
    openImageCaptureDialog() {
      // Open the image capture dialog
      this.showImageCaptureDialog = true;
    },
    handleImageCaptured(base64Image) {
      // Handle the captured image (base64Image)
      this.imageSrc = base64Image;
    },
  },
};
</script>
<template>
  <div class="fixed inset-0 flex items-center justify-center z-10 ">
    <div class="bg-gray-200 p-4 rounded-lg border outline-1 border-stone-700 min-w-max">
      <!-- Your content goes here -->
      <button class="p-1 rounded-md border outline-1 border-gray-600" @click="closeModal">
        <Icon name="material-symbols:close-rounded" />
      </button>

      <div class="p-3 bg-orange-200">
        <!-- // here -->
        <div class="camera-button flex justify-evenly mb-2">
          <button type="button" class="button p-2 rounded-md bg-green-500 hover:bg-green-600" @click="openCamera">
            <span v-if="!isCameraOpen">Open Camera</span>
            <span v-else>Close Camera</span>
          </button>
          <button class="p-2 rounded-md bg-green-500 hover:bg-green-600" id="snap" v-on:click="capture()">
            Snap Photo
          </button>
          <button class="p-2 rounded-md bg-green-500 hover:bg-green-600" id="snap" v-on:click="toggleImagesList()">
            <span v-if="!displayImages">Show all Images</span>
            <span v-else>Hide Images</span>
          </button>
          <button class="p-2 rounded-md bg-green-500 hover:bg-green-600" id="snap" v-on:click="deleteImages()">
            Delete Images
          </button>
        </div>
        <div id="el" class="text-center">
          <div class="text-center mx-auto">
            <video class="mx-auto rounded-md" ref="video" id="video" width="180" height="130" autoplay></video>
          </div>

          <canvas class="mx-auto my-2 rounded-md text-center" ref="canvas" id="canvas"></canvas>
          <ul v-if="displayImages" class="flex flex-wrap justify-evenly">
            <p v-if="captures.length == 0"> No Images to show </p>
            <li v-for="c in captures">
              <img v-bind:src="c" height="1" />
            </li>
          </ul>
        </div>




      </div>
    </div>

  </div>
</template>

<script>
export default {

  data() {
    return {
      video: {},
      canvas: {},
      captures: [],
      isCameraOpen: false,
      isPhotoTaken: false,
      isShotPhoto: false,
      isLoading: false,
      link: '#',
      displayImages: false,
    };
  },
  mounted() {

  },
  methods: {

    closeModal () {
      this.openCamera();
      this.$emit('close-modal');
      
    },
    deleteImages() {
      this.captures = [];
    },

    toggleImagesList() {
      this.displayImages = !this.displayImages;
    },

    openCamera() {
      if (this.isCameraOpen) {
        this.closeCamera();
      } else {

        this.video = this.$refs.video;
        if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
          navigator.mediaDevices.getUserMedia({ video: true, audio: false }).then(stream => {
            console.log(stream)
            video.srcObject = stream;
            this.video.play();
            this.isCameraOpen = true;
          });
        }
      }
    },
    closeCamera() {
      let tracks = this.$refs.video.srcObject.getTracks();

      tracks.forEach(track => {
        track.stop();
      });
      this.isCameraOpen = false;
    },

    capture() {
      if (!this.isCameraOpen) {
        console.log('camera is not open');
        return;
      }
      this.canvas = this.$refs.canvas;
      var context = this.canvas
        .getContext("2d")
        .drawImage(this.video, 0, 0, 200, 160);
      this.captures.push(canvas.toDataURL("image/png"));
      console.log(this.captures)
    },
  }
}
</script>

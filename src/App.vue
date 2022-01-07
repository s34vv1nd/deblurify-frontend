<template>
  <h1>DEBLURIFY</h1>
  <input
    type="file"
    accept="image/jpeg/*"
    @change="uploadImage()"
  />
  <div class="img-container">
    <img class="upload-img" id="upload-img" :src="rawImg" alt="your original image" />
    <button class="deblur-btn" title="Deblurify" @click="deblurify()">
      Deblurify
    </button>
    <img class="deblur-img" id="deblur-img" :src="deblurifiedImg" alt="your deblurified image" />
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: 'App',
  components: {
  },

  data() {
    return {
      deblurifiedImg: null,
      rawImg: null,
    }
  },

  mounted() {
    // axios.get("http://localhost:8080/api/v1/deblur").then(response => {
    //   console.log(response)
    // })
  },

  methods: {
    uploadImage() {
      const file = document.querySelector('input[type=file]').files[0]
      const reader = new FileReader()

      reader.onloadend = () => {
        this.rawImg = reader.result;
        // console.log(this.rawImg);
      }
      reader.readAsDataURL(file);
      // console.log(file)
    },

    deblurify() {
      if (!this.rawImg) return;
      axios.post("http://localhost:8080/api/v1/deblur", {
        image: this.rawImg
      }).then((response) => {
        // console.log(response)
        this.deblurifiedImg = response.data.image
        console.log(this.deblurifiedImg)
      })
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.upload-img {
  max-width: 40rem;
  max-height: 40rem;
}
.deblur-img {
  max-width: 40rem;
  max-height: 40rem;
}
.deblur-btn {
  margin: 5rem;
}
</style>

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
    this.rawImg = localStorage.getItem("RAW_IMG")
    this.deblurifiedImg = localStorage.getItem("DEBLURIFIED_IMG")
  },

  methods: {
    uploadImage() {
      const file = document.querySelector('input[type=file]').files[0]
      const reader = new FileReader()

      reader.onloadend = () => {
        this.rawImg = reader.result;
        localStorage.setItem("RAW_IMG", this.rawImg)
      }
      reader.readAsDataURL(file);
    },

    deblurify() {
      if (!this.rawImg) return;
      axios.post("http://localhost:8080/api/v1/deblur", {
        image: this.rawImg
      }).then((response) => {
        this.deblurifiedImg = `data:image/jpeg;base64,${response.data.image}`
        localStorage.setItem("DEBLURIFIED_IMG", this.deblurifiedImg)
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

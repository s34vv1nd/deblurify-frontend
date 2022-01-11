<template>
  <h1>WELCOME TO DEBLURIFY WEB APP!</h1>

  <label class="custom-select" for="styledSelect1"
    ><select id="styledSelect1" name="options">
      <option value="">Choose your deblurify option</option>
      <option value="1">Fast</option>
      <option value="2">Beautiful</option>
      <option value="3">Experiment</option>
    </select></label
  >

  <label class="custom-file-upload button-76">
    <input type="file" accept="image/jpeg/*" @change="uploadImage()" />
    <i class="fa fa-cloud-upload"></i> Upload your image
  </label>

  <div class="img-container">
    <img
      class="upload-img imgBorder image-one"
      id="upload-img"
      :src="rawImg"
      width="400"
      height="600"
      alt="your original image"
    />
    <button class="deblur-btn button-76" title="Deblurify" @click="deblurify()">
      Deblurify
    </button>
    <img
      class="deblur-img imgBorder upload-img image-two"
      id="deblur-img"
      :src="deblurifiedImg"
      width="400"
      height="600"
      alt="your deblurified image"
    />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},

  data() {
    return {
      deblurifiedImg: require("@/assets/deblured-image.png"),
      rawImg: require("@/assets/original-image.png"),
    };
  },

  mounted() {
    // axios.get("http://localhost:8080/api/v1/deblur").then(response => {
    //   console.log(response)
    // })
    //this.rawImg = localStorage.getItem("RAW_IMG");
    //this.deblurifiedImg = localStorage.getItem("DEBLURIFIED_IMG");
  },

  methods: {
    uploadImage() {
      const file = document.querySelector("input[type=file]").files[0];
      const reader = new FileReader();

      reader.onloadend = () => {
        this.rawImg = reader.result;
        localStorage.setItem("RAW_IMG", this.rawImg);
      };
      reader.readAsDataURL(file);
    },

    deblurify() {
      if (!this.rawImg) return;
      let deblurType = document.getElementById("styledSelect1").value;

      if (deblurType == 1) {
        axios
          .post("http://localhost:8080/api/v1/deblur", {
            image: this.rawImg,
          })
          .then((response) => {
            this.deblurifiedImg = `data:image/jpeg;base64,${response.data.image}`;
            localStorage.setItem("DEBLURIFIED_IMG", this.deblurifiedImg);
          });
      } else if (deblurType == 2) {
        axios
          .post("http://localhost:8080/api/v1/deblur", {
            image: this.rawImg,
          })
          .then((response) => {
            this.deblurifiedImg = `data:image/jpeg;base64,${response.data.image}`;
            localStorage.setItem("DEBLURIFIED_IMG", this.deblurifiedImg);
          });
      } else if (deblurType == 3) {
        axios
          .post("http://localhost:8080/api/v1/deblur", {
            image: this.rawImg,
          })
          .then((response) => {
            this.deblurifiedImg = `data:image/jpeg;base64,${response.data.image}`;
            localStorage.setItem("DEBLURIFIED_IMG", this.deblurifiedImg);
          });
      }
    },
  },
};
</script>

<style>
html {
  background: linear-gradient(to right, #29323c, #485563);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: linear-gradient(to right, #29323c, #485563);
  height: 1000px;
}

h1 {
  color: white;
  margin-bottom: 54px;
}

.imgInput {
  margin-bottom: 100px;
}

.upload-img {
  max-width: 40rem;
  max-height: 40rem;
  margin-bottom: 20px;
}
.deblur-btn {
  margin: 5rem;
  position: absolute;
  top: 500px;
  right: 788px;
}

.image-one {
  position: absolute;
  top: 400px;
  right: 1280px;
}

.image-two {
  position: absolute;
  top: 400px;
  right: 200px;
}

.imgBorder {
  padding: 15px 15px 0;
  background-color: white;
  box-shadow: 0 1px 3px rgba(34, 25, 25, 0.4);
  -moz-box-shadow: 0 1px 2px rgba(34, 25, 25, 0.4);
  -webkit-box-shadow: 0 1px 3px rgba(34, 25, 25, 0.4);
}
input[type="file"] {
  display: none;
}
.custom-file-upload {
  margin-top: 100px;
  border: 1px solid #ccc;
  display: inline-block;
  padding: 6px 12px;
  cursor: pointer;
  margin-bottom: 40px;
  border-radius: 5%;
}

.button-76 {
  background-color: #cf245f;
  background-image: linear-gradient(to bottom right, #fcd34d, #ef4444, #ec4899);
  border: 0;
  border-radius: 0.25rem;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  font-family: ui-sans-serif, system-ui, -apple-system, system-ui, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif,
    "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  font-size: 1.125rem; /* 18px */
  font-weight: 600;
  line-height: 1.75rem; /* 28px */
  padding: 1rem 1.25rem;
  text-align: center;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-76:hover {
  box-shadow: none;
}

@media (min-width: 1024px) {
  .button-76 {
    font-size: 1.5rem; /* 24px */
    padding: 1rem 1.5rem;
    line-height: 2rem; /* 32px */
  }
}

.custom-select {
  position: relative;
  display: block;
  max-width: 400px;
  min-width: 180px;
  margin: 0 auto;
  border: 1px solid #3c1c78;
  background-color: #16013e;
  z-index: 10;
}
select {
  border: none;
  outline: none;
  background: transparent;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border-radius: 0;
  margin: 0;
  display: block;
  width: 100%;
  padding: 12px 55px 15px 15px;
  font-size: 14px;
  color: #714bb9;
}
select::after {
  position: absolute;
  right: 0;
  top: 0;
  width: 50px;
  height: 100%;
  line-height: 38px;
  content: "∨";
  text-align: center;
  color: white;
  font-size: 24px;
  border-left: 1px solid #3c1c78;
  z-index: -1;
}
</style>

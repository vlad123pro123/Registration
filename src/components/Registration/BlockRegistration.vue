<script setup>
import { defineProps, ref } from "vue";

const model = defineModel();

const props = defineProps( {
  label: {
    type: String,
    required: true
  },
  img: {
    type: String,
    required: true
  },
  idInput:{
    type:String,
    required:true
  },
  Placeh:{
    type:String,
    required:true
  },
  types:{
    type:String,
    required:true
  },
  ImgGlaz:{
    type:String,
    required:true
  },
  initialType: {
    type: String,
    default: 'password'
  }
});
const inputType = ref(props.initialType);

const isShowPassword = ref(false);
</script>

<template>
  <div class="input-container">
      <i class="fa fa-search"> <img :src="img" alt="#"></i>
      <div class="block-input-label">
        <span>{{label}}</span>
        <input :type="isShowPassword? 'text' : inputType" :id="idInput" label="inputField" :placeholder="Placeh" v-model="model">
      </div>
      <img @click="isShowPassword = true" class="password-control" :src="ImgGlaz">
  </div>
</template>

<style scoped>
.password-control{
  margin-left: 5%;
  cursor: pointer;
}
.input-container {
  position: relative;
  width: 90%;
  height: 70px;
  border-radius: 10px;
  background: rgba(0, 0, 0, 0.3);
  padding: 10px;
  display: flex;
  align-items: center;
}
.block-input-label {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 44px;
  margin-left: 15px;
  align-items: start;
}
.input-container input {
  width: 95%;
  height: 100%;
  border: none;
  background: transparent;
  color: rgb(255, 255, 255);
  font-family: Manrope;
  font-size: 20px;
  font-weight: 600;
  line-height: 27px;
  outline: none;
}

.input-container label {
  position: absolute;
  top: 0;
  left: 10px;
  color: white;
  font-size: 14px;
}
.fa-search{
  margin-left: 20px;
  margin-top: 6px;
}
.fa-search img{
  width: 30px;
}
span{
  color: rgb(116, 116, 116);
  font-family: Manrope;
  font-size: 13px;
  font-weight: 600;
  line-height: 18px;
}
</style>
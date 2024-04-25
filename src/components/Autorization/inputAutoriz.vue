<script setup>

import { defineProps, ref } from "vue";

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
  show:{
    type:Boolean,
    required:true
  }
});

const togglePassword = () => {
  props.show = true;
};
</script>

<template>
  <div class="container-autorization">
    <i class="fa fa-search"> <img :src="img" alt="#"></i>
    <div class="block-input-label">
      <span>{{label}}</span>
      <input :type="types" :id="idInput"  label="inputField" :placeholder="Placeh">
    </div>
    <img @click="togglePassword"  class="password-control" :src="ImgGlaz">
  </div>
</template>

<style scoped>
.password-control{
  margin-left: 5%;
  cursor: pointer;
}
.container-autorization {
  position: relative;
  width: 90%;
  height: 18%;
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
.container-autorization input {
  height: 100%;
  border: none;
  background: transparent;
  color: rgb(255, 255, 255);
  font-family: Manrope;
  font-size: 20px;
  font-weight: 600;
  line-height: 27px;
  outline: none;
  width: 95%;
}

.container-autorization label {
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
span{
  color: rgb(116, 116, 116);
  font-family: Manrope;
  font-size: 13px;
  font-weight: 600;
  line-height: 18px;
}
</style>
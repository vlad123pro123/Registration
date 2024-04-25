<script setup>

</script>

<template>
  <div class="container-message-error">
    <i class="error"><img src="@/assets/img/Activ.svg"></i>
    <div class="block-txt-error">
      <h4>Регистрация прошла успешно</h4>
    </div>
  </div>
</template>

<style scoped>

.container-message-error{
  width: 251px;
  height: 65px;
  box-sizing: border-box;
  border: 1.5px solid rgb(62, 186, 60);
  border-radius: 10px;
  background: rgba(0, 0, 0, 0.3);
  opacity: 0.9;
  display: flex;
  align-items: center;
  gap:15px;
}
.error{
  margin-left: 20px;
}
span{
  color: rgb(161, 161, 161);
  font-family: Manrope;
  font-size: 10px;
  font-weight: 600;
  line-height: 14px;
  text-align: left;
}
h4{
  color: rgb(255, 255, 255);
  font-family: Manrope;
  font-size: 13px;
  font-weight: 600;
  line-height: 18px;
  text-align: left;
}
</style>
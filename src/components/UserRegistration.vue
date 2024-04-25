<script setup>
import BlockRegistration from "@/components/Registration/BlockRegistration.vue";
import user from "../assets/img/user.svg"
import email from "../assets/img/email.svg"
import password from "../assets/img/key.svg"
import glaz from "../assets/img/glaz.svg"
import InputAutoriz from "@/components/Autorization/inputAutoriz.vue";
import MessageError from "@/components/Message/MessageError.vue";
import MessageSuccessful from "@/components/Message/MessageSuccessful.vue";
import ResetInput from "@/components/Reset/ResetInput.vue";
import {reactive, ref} from "vue";

const showPassword = ref(false);
const showPanel = reactive( {
  isActiveOne:true,
  hasErrorTwo:true,
  MesErrorNott:true,
  MesSuccesNott:true,
  hasErrorRest:true,
  isActivePaneReg:true
});

const UserPaswordOne = ref('');
const UserPaswordTwo = ref('');
const UserLogin = ref('');
const UserEmail = ref('');
const PanelErrorMes = ref('')
const isValidEmail = ref(true);

function OnRegistr() {
  showPanel.isActiveOne = true;
  showPanel.hasErrorTwo = true;
  showPanel.isActiveTwo = false;
  showPanel.hasErrorOne = false;
}

function OnAutoriz() {
  showPanel.isActiveTwo = true;
  showPanel.isActiveOne = false;
  showPanel.hasErrorTwo = false;
  showPanel.hasErrorOne = true;
}

function OnLok() {
  showPanel.MesSuccesNott = false;
  showPanel.MesErrorNott = true;
}

function ForgotPasword() {
  showPanel.hasErrorPaneReg = true;
  showPanel.isActiveRest = true;
  showPanel.hasErrorRest = false;
}
function closeForgot(){
  showPanel.hasErrorPaneReg = false;
  showPanel.isActiveRest = false;
  showPanel.hasErrorRest = true;
}
function OnError(messagh) {
  showPanel.MesErrorNott = false;
  showPanel.MesSuccesNott = true;
  PanelErrorMes.value = messagh;

}
const validateEmail = () => {
  const emailRegex = /^([A-Za-z0-9_\-.])+@([A-Za-z0-9_\-.])+\.([A-Za-z]{2,4})$/;
  isValidEmail.value = emailRegex.test(UserEmail.value);
};
function Reg() {
  validateEmail();

  if (UserPaswordOne.value !== UserPaswordTwo.value) {
    OnError('Пароли не совпадают');
  } else if (!UserLogin.value || !UserEmail.value || !UserPaswordOne.value || !UserPaswordTwo.value) {
    OnError('Не заполненное поле');
  } else if (!isValidEmail.value) {
    OnError('Не правильный email');
  } else if (UserPaswordOne.value.length < 7) {
    OnError('Маленький пароль');
  } else {
    OnLok();
  }
}

const inputType = ref('password');
const TypeLogEmail = ref('text');
</script>

<template>
<div class="container-registration" :class="{ActivePaneReg : showPanel.isActivePaneReg, closePaneReg: showPanel.hasErrorPaneReg }">
  <div class="block-reg">
    <div class="block-button">
      <button @click="OnRegistr" class="button-registration" :class="{ active: showPanel.isActiveOne, noactive:showPanel.hasErrorOne }">Регистрация</button>
      <button @click="OnAutoriz" class="button-autriz" :class="{ activev: showPanel.isActiveTwo, noactivev:showPanel.hasErrorTwo }">Авторизация</button>
    </div>
    <div class="block-input" :class="{ activeOne: showPanel.isActiveOne, closeOne: showPanel.hasErrorOne }">
      <BlockRegistration label="Введите логин" v-model="UserLogin" :initialType="TypeLogEmail" :img="user" idInput="login" Placeh="Vlad123pros" />
      <BlockRegistration label="Введите E-mail" v-model="UserEmail" :initialType="TypeLogEmail" :img="email" idInput="email" Placeh="Vlad@gmail.com"/>
      <BlockRegistration label="Введите пароль" v-model="UserPaswordOne" :initialType="inputType" :img="password" idInput="pasword" Placeh="******" :ImgGlaz="glaz"/>
      <BlockRegistration label="Повторите" v-model="UserPaswordTwo" :initialType="inputType" :img="password" idInput="RepPasword" Placeh="*******" :ImgGlaz="glaz"/>
      <button @click="Reg" class="but-zareg">Зарегистрироваться</button>
    </div>
    <div class="block-input-autoriz" :class="{ activeTwo: showPanel.isActiveTwo, closeTwo: showPanel.hasErrorTwo }">
      <InputAutoriz label="Введите логин" types="text" :img="user" idInput="logAutoriz" Placeh="Vlad123pros"/>
      <InputAutoriz label="Введите пароль" :types="showPassword ? 'text' : 'password'" :img="password" idInput="LogPasword" Placeh="*******" :ImgGlaz="glaz"/>
      <div class="container-save-pasword">
        <div class="block-save-pasword">
          <input type="checkbox" id="rememberMe">
          <label for="rememberMe">Запомнить меня</label>
        </div>
        <a class="restoration-pasword" @click="ForgotPasword">Забыли пароль?</a>
      </div>
      <button class="btn-autoriz">Авторизоваться</button>
    </div>
  </div>
  <div class="block-image">
    <img src="../assets/img/zombi.png" alt="#">
  </div>
</div>
  <div class="container-ForgotPassword" :class="{ActiveRest : showPanel.isActiveRest, closeRest: showPanel.hasErrorRest }">
    <div class="block-ForgotPassword">
      <h3>Востановление пароля</h3>
      <ResetInput class="ResetInput"  types="text" Placeh="Vlad123pro" idInput="ForPasword" :img="user" label="Логин/Email"/>
      <span>На ваш E-mail будет отправлено письмо содержащее новый пароль от аккаунта</span>
      <span class="close-btn" @click="closeForgot"><-Вернуться назад</span>
      <button class="reset-btn">Сбросить пороль</button>
    </div>
  </div>
  <div class="container-massage">
    <MessageError :text="PanelErrorMes" :class="{ MesErrorActiv: showPanel.MesErrorActivv, MesErrorNot: showPanel.MesErrorNott }"/>
    <MessageSuccessful :class="{ MesSuccesActiv: showPanel.MesSuccesActivv, MesSuccesNot: showPanel.MesSuccesNott }"/>
  </div>
</template>

<style scoped>
.ActiveRest{
  display: flex;
}

.closeRest{
  display: none;
}

.ActivePaneReg{
  display: flex;
}

.closePaneReg{
  display: none;
}

.block-image img{
  width: 100%;
  height: 100%;
}
.ResetInput{
  margin-top: 20px;
}
.close-btn:hover{
  cursor: pointer;
  opacity: 0.3;
}
span{
  color: rgb(255, 255, 255);
  font-family: Manrope;
  font-size: 13px;
  font-weight: 500;
  line-height: 18px;
}
h3{
  color: rgb(255, 255, 255);
  font-family: Manrope;
  font-size: 20px;
  font-weight: 600;
  line-height: 27px;
  text-align: center;
}
.block-ForgotPassword{
  width: 78%;
  height: 90%;
  margin: auto;
  display: flex;
  flex-direction: column;
  margin-top: 20px;
  gap: 15px;
}
.reset-btn{
  width: 100%;
  height: 15%;
  border-radius: 10px;
  background: rgb(252, 104, 84);
}
.container-ForgotPassword{
  width: 35%;
  height: 40%;
  border-radius: 10px;
  background: rgba(23, 24, 28, 0.9);
  margin: auto;

}
.MesErrorNot{
  display:none;
}
.MesErrorActiv{
  display:flex;
}

.MesSuccesActiv{
  display:flex;
}
.MesSuccesNot{
  display:none;
}
.btn-autoriz{
  width: 90%;
  height: 15%;
  border-radius: 10px;
  background: rgb(252, 104, 84);
}
.block-save-pasword {
  display: flex;
  align-items: center;
}
.container-massage{
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}
.restoration-pasword{
  color: rgb(116, 116, 116);
  font-family: Manrope;
  font-size: 13px;
  font-weight: 500;
  line-height: 18px;
  text-align: left;
  cursor: pointer;
}
.block-save-pasword label{
  color: rgb(255, 255, 255);
  font-family: Manrope;
  font-size: 13px;
  font-weight: 500;
  line-height: 18px;
  text-align: left;
}
/* Стилизация чекбокса */
.block-save-pasword input[type="checkbox"] {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  width: 25px;
  height: 25px;
  box-sizing: border-box;
  border: 2px solid rgb(252, 104, 84);
  border-radius: 8px;
  margin-right: 10px;
  cursor: pointer;
}

/* Кастомный стиль для выбранного чекбокса */
.block-save-pasword input[type="checkbox"]:checked::before {
  content: "\2714"; /* Unicode для галочки */
  display: inline-block;
  width: 20px;
  height: 25px;
  text-align: center;
  line-height: 20px;
  background-color: rgba(51, 51, 51, 0);
  color: rgb(252, 104, 84);;
  border-radius: 5px;
}

.but-zareg{
  width: 90%;
  height: 15%;
  border-radius: 10px;
  background: rgb(252, 104, 84);
}
.container-registration{
  width: 65%;
  height: 70%;
  border-radius: 10px;
  background: rgba(23, 24, 28, 0.9);
  margin: auto;
}
.container-save-pasword{
  display: flex;
  justify-content: space-between;
  margin-right: 60px;
  align-items: center;
}
.block-input{
  margin-left: 60px;
  margin-top: 40px;
  margin-bottom: 40px;
  height: 100%;
  flex-direction: column;
  justify-content: space-between;
}
.block-input-autoriz{
  margin-left: 60px;
  margin-top: 40px;
  margin-bottom: 40px;
  height: 100%;
  flex-direction: column;
  gap: 40px;
  justify-content: center;
}
.block-reg{
  width: 50%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.block-button{
  display: flex;
}
button{
  width: 293px;
  cursor: pointer;
  height: 67px;
  color: rgb(255, 255, 255);
  font-family:Manrope;
  font-size: 20px;
  font-weight: 600;
  line-height: 27px;
  text-align: center;
}
.button-registration{
  border-radius: 10px 0px 0px 0px;
}
</style>
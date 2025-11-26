
<template>

    <!-- FORM -->

<div class="container">
    <div class="form">
    <h2 class="form">Форма регистрации</h2>
    <form @submit.prevent="submitForm">
            <input v-model="name" type="text" placeholder="Введите имя" />
            <input v-model="email" type="email" placeholder="Введите email" />
            <input v-model="password" type="password" placeholder="Придумайте пароль" />
        <button type="submit">Отправить</button>
    </form>
    <p v-if="submitted">
        Отправлено
    </p>
    </div>

    <!--COUNTER-->
    <h2 class="header-counter">Счетчик</h2>
    <div>
        <img src="/rolls.jpg" class="roll" alt="">
    </div>
    <div class="counter">
    <button class="button-counter" @click="decrease">−</button>
    <span>{{ count }}</span>
    <button class="button-counter" @click="increase">+</button>
    </div>

    <!--CALCULATOR-->
    <h2 class="calculator">Калькулятор</h2>
<div class="calc">
    <!-- экран -->
    <div class="calc-screen">
        <p>{{ display }}</p>
    </div>

    <!-- кнопки -->
    <div class="buttons">
        <div class="btn ac white" @click="clearAll">AC</div>
        <div class="btn plus-minus white" @click="plusMinus">+/-</div>
        <div class="btn procent white" @click="percent">%</div>
        <div class="btn division bg-pink" @click="pressAction('/')">/</div>
        <div class="btn seven purple" @click="pressDigit('7')">7</div>
        <div class="btn eight purple" @click="pressDigit('8')">8</div>
        <div class="btn nine purple" @click="pressDigit('9')">9</div>
        <div class="btn myltiply bg-pink" @click="pressAction('X')">X</div>

        <div class="btn four purple" @click="pressDigit('4')">4</div>
        <div class="btn five purple" @click="pressDigit('5')">5</div>
        <div class="btn six purple" @click="pressDigit('6')">6</div>
        <div class="btn minus bg-pink" @click="pressAction('-')">-</div>

        <div class="btn one purple" @click="pressDigit('1')">1</div>
        <div class="btn two purple" @click="pressDigit('2')">2</div>
        <div class="btn three purple" @click="pressDigit('3')">3</div>
        <div class="btn plus bg-pink" @click="pressAction('+')">+</div>

        <div class="btn zero purple" @click="pressDigit('0')">0</div>
        <div class="btn dot purple" @click="pressDigit('.')">.</div>
        <div class="btn equal bg-pink" @click="calculate">=</div>
    </div>
</div>

</div>

</template>

<style scoped>
/* FORM */
.container {
    max-width: 400px;
    display: flex;
    margin: 0 auto;
    flex-direction: column;
    gap: 20px;
}
.form {
    max-width: 250px;
    display: flex;
    flex-direction: column;
    gap: 10px;
}
input {
    width: 100%;
    padding: 8px;
    border-radius: 20px;
    border: none;
    outline: none;
    margin-top: 15px;

}
button {
    margin-top: 20px;
    border: none;
    background-color: blueviolet;
    color: white;
    padding: 10px 32px;
    text-align: center;
    text-decoration: none;
    border-radius: 20px;
}
.form {
    color: blueviolet;
}

/* COUNTER */

.header-counter {
    color: olive;
}
.roll {
    width: 200px
}
.counter {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 20px;
    
}
.counter span {
    min-width: 30px;
    text-align: center;
    font-weight: bold;
}

.button-counter {
    margin: 0;
    background-color: olive;
}
/* CALCULATOR */

.calculator {
    color:#cc93b9;
}
.calc {
    width: 300px;
    height: 500px;
    border-radius: 20px;
    background-color:#cc93b9;
    color: #fff;
    font-family: Arial;
    padding: 18px;
    box-shadow: 4px 4px 4px #cc93b9;

}
.calc-screen {
    height: 125px;
    padding: 10px;
    display: flex;
    justify-content: end;
    align-items: end;
    margin-bottom: 25px;
}

.calc-screen p {
    text-align: right;
    font-size: 4rem;
    margin: 0;
    

}

.buttons {
    display: grid;
    grid-template-areas:
    "ac plus-minus percent division"
    "seven eight nine multi"
    "four five three plus"
    "one two three plus"
    "zero zero dot equal";
    grid-gap: 7px;
    justify-items: center;

}
.btn {
    width: 60px;
    height: 60px;
    background-color:#690849;
    border-radius: 40px;
    text-align: center;
    line-height: 60px;
    font-size: 1.5em;
    cursor: pointer;
    user-select: none;
}

.btn.zero {
    grid-area: zero;
    width: 100%;
    border-radius: 34px;
}
.btn:hover {
    filter: brightness(120%);
}

.btn:active {
    filter: brightness(90%);
}

.btn.bg-pink {
    background-color:#b42082 ;
}

.btn.white {
    background-color:#ffffff ;
    color: #690849;
}

</style>

<script setup>

//FORM

import { ref } from "vue"

const name = ref("")
const email = ref("")
const password = ref("")
const submitted = ref(false)

function submitForm() {
    console.log("Имя:", name.value)
    console.log("Email:", email.value)
    console.log("Пароль:", password.value)
    
    submitted.value = true
}

// COUNTER


const count = ref(1)  // стартовое значение

function increase() {
    count.value++
}

function decrease() {
    if (count.value > 1) count.value--
}

// CALCULATOR

// переменные калькулятора
const a = ref('')
const b = ref('')
const sign = ref('')
const finish = ref(false)

// экран
const display = ref('0')

// функции
function clearAll() {
    a.value = ''
    b.value = ''
    sign.value = ''
    finish.value = false
    display.value = '0'
}

function pressDigit(digit) {
  if (finish.value) { // если только что закончили вычисление
    a.value = ''
    finish.value = false
}
if (!sign.value) {
    a.value += digit
    display.value = a.value
} else {
    b.value += digit
    display.value = b.value
}
}

function pressAction(op) {
    if (!a.value) return
    sign.value = op
}

function calculate() {
    if (!b.value) return
    let result
    const numA = parseFloat(a.value)
    const numB = parseFloat(b.value)
    switch(sign.value) {
    case '+': result = numA + numB; break
    case '-': result = numA - numB; break
    case 'X': result = numA * numB; break
    case '/': result = numB !== 0 ? numA / numB : 'Error'; break
}

display.value = result
a.value = result.toString()
b.value = ''
sign.value = ''
finish.value = true
}

// дополнительные функции
function plusMinus() {
    if (!sign.value) {
        a.value = (-parseFloat(a.value || 0)).toString()
        display.value = a.value
    } else {
        b.value = (-parseFloat(b.value || 0)).toString()
        display.value = b.value
    }
}

function percent() {
    if (!sign.value) {
        a.value = (parseFloat(a.value || 0) / 100).toString()
        display.value = a.value
    } else {
        b.value = (parseFloat(b.value || 0) / 100).toString()
        display.value = b.value
    }
}
</script>
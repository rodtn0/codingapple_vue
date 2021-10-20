<template>

<!-- 모달 -->
  <transition name="fade">
    <Modal @closeModal="모달창열렸니=false"
           :원룸들="원룸들" :누른거="누른거"
           :모달창열렸니="모달창열렸니" />
  </transition>

  <!-- 메뉴 -->
  <div class="menu">
    <a v-for="a in 메뉴들" :key="a"> {{ a }} </a>
  </div>

  <Discount v-if="showDiscount == true"/>
  <p>지금 결제하면 {{ amount }}% 할인</p>

  <button @click="priceSort">가격순정렬</button>
  <button @click="priceReverse">가격역순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card @openModal="모달창열렸니 = true; 누른거 = $event"
        :원룸="원룸들[i]" v-for="(원룸, i) in 원룸들" :key="원룸"/>

  <!-- 상품 -->
<!--  <div v-for="(a, i) in 원룸들" :key="i">-->
<!--    <img :src="a.image" class="room-img">-->
<!--    <h4 @click="모달창열렸니 = true; 누른거 = i">상품명 : {{ a.title }}</h4>-->
<!--    <p>가격 : {{ a.price }}원</p>-->
<!--  </div>-->

</template>

<script>
import data from './assets/oneroom';
import Discount from "./Discount";
import Modal from "./Modal";
import Card from "./Card";

export default {
  name: 'App',
  data(){
    return{
      amount : 30,
      showDiscount : true,
      원룸들오리지널 : [...data],
      오브젝트 : {name : 'kim', age : 20},
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
      prices : ['50만원', '60만원', '70만원'],
      스타일 : 'color : steelblue',
      신고수 : [0, 0, 0],
    }
  },
  methods:{
    increase(){
      this.신고수 += 1;
    },
    priceSort(){
      this.원룸들.sort(function (a, b){
        return a.price - b.price
      });
    },
    priceReverse(){
      this.원룸들.reverse(function (a, b){
        return a.price - b.price
      });
    },
    sortBack(){
      this.원룸들 = [...this.원룸들오리지널];
    }
  },
  created() {
  },
  mounted() {
    setTimeout(()=>{
      this.showDiscount = false;
    }, 2000),
    setInterval(()=>{
      this.amount--;
    }, 1000);
  },
  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
.fade-enter-from{
  transform: translateY(-1000px);
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  transform: translateY(0px);
}
.fade-leave-from{
  opacity: 1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  opacity: 0;
}
body{
  margin: 0;
}
div{
  box-sizing: border-box;
}
.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}
.white-bg{
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.room-img{
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>

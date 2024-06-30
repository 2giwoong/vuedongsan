<template>
  <transition name="fade">
    <ModalComponent @closeModal = "modal = false" :onerooms = "onerooms" :clickContent = "clickContent" :modal = "modal"/>
  </transition>
  <div class="menu">
    <a v-for="menu in menus" :key="menu">{{ menu }}</a>
    <!-- key는 반복문 돌린요소를 컴퓨터가 구분하기 위해 사용하는 것으로 반복문 쓸떄 꼭 사용해야함 -->
    <!-- vue반복문은 변수 작명 2개까지 가능 -->
  </div>
  <!-- <div v-for="(a,i) in 3" :key="i">
    <h4 >{{ products[i] }}</h4>
    <p>60 만원</p>
  </div> -->
  <DiscountComponent v-if="showDiscount == true" :amount = "amount"/>
  <button @click="priceSort">가격순정렬</button>
  <button @click="priceBack">되돌리기</button>
  <CardComponent @openModal="modal = true; clickContent = $event" v-for="(oneroom, i) in onerooms" :key="oneroom" :oneroom = "onerooms[i]"/>
</template>

<script>
import { data } from './assets/oneroom';
import CardComponent from './CardComponent.vue';
import DiscountComponent from './DiscountComponent.vue';
import ModalComponent from './ModalComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      showDiscount: true,
      amount: 5,
      oneroomsOriginal: [...data],// 동일한 data가 2개이면 안되니 사본을 만들어 사용해야해서 ...을사용
      clickContent: 0,
      onerooms: data,
      modal: false,
      num: [0, 0, 0],
      menus : ['Home','Shop', 'About'],
    }
  },
  methods: {
    increase() {
      this.num += 1 //함수안에서 데이터 쓸때는 this.데이터명 입력하기
    },
    priceSort() {
      // var array = [3,5,2];
      // array.sort(function(a,b) {// a,b칸이 배열의 데이터가 들어가는 칸이고 데이터 2개씩 비교를해서 a - b가 음수면 왼쪽 양수면 오른쪽으로 끝까지 비교해 순차나열하는 것 
      //   return a - b
      // })
      this.onerooms.sort(function(a,b) {
        return a.price - b.price//onerooms 배열 안의 데이터를 가져와서 붙여주면됨
      });
    },
    //sort함수를 쓰면 원본이 변형됨, map(), filter() 등은 원본을 보존해줌
    priceBack() {
      this.onerooms = [...this.oneroomsOriginal]// 두개의 배열에 부등호를 사용하면 몇번은 작동하지만 결국 onerooms와 oneroomsOriginal이 같아지면서 동일한 data가 되어버려 오작동이남 그래서 여기에서도 ...을 사용하여 사본을 만들어주기
    }
  },
  /*beforeMount() {

  },//마운트 되기 전
  mounted() {
    setTimeout(() => {
      this.showDiscount = false;
    },2000)
  },//마운트 된 후*/
  mounted() {
    setInterval(() => {
      if(this.amount > 0) {
        this.amount --;
      } else {
        clearInterval();
      }
    }, 1000);
  },
  components: {
    DiscountComponent, //Discount: Discount 로 써도 되는데 es6문법으로 한번만 써도 상관x
    ModalComponent,
    CardComponent
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin:0;
  padding:0;
}
.menu {
  background: darksalmon;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: #fff;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.discount {
  background-color: #eee;
  padding: 10px;
}
.black-bg {
  position: fixed;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,.5);
  padding: 20px;
}
.white-bg {
  width: 100%;
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
.fade-enter-from {
  opacity: 0;
}/*fade칸에 작명하면됨 */
.fade-enter-active {
  transition: all 1s ease;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s ease;
}
.fade-leave-to {
  opacity: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

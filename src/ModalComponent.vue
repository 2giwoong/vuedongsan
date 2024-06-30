<template>
  <div class="black-bg" v-if="modal == true">
    <div class="white-bg">
      <h4>{{ onerooms[clickContent].title }}</h4>
      <p>{{ onerooms[clickContent].content }}</p>
      <!-- <button @click="modal = false">닫기</button>이벤트로 props를 수정하고 있는데 props는 읽어오는 것만 가능하고 수정은 안되어서 컴포넌트에서 사용불가 -->
      <input v-model="month"><!-- input 에 입력한 값을 데이터로 저장할땐 v-model 사용 -->
      <input type="range" min="1" max="12">
      <p>{{ month }}개월 선택함 : {{ onerooms[clickContent].price * month}}원</p> 
      <button @click="closeModal">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name : 'ModalComponent',
  props : {
    onerooms: Array,
    clickContent: Number,
    modal: Boolean,
  },
  data() {
    return {
      month : 1,
    }
  },
  watch : {// 데이터 감시할때 사용함
    month(a) {
      //month라는 데이터가 변할때 해당 코드 실행
      if(isNaN(a) == true) {
        alert('글 ㄴㄴ');
        this.month = 1;
      }
    }
  },
  methods : {
    closeModal() {
      this.$emit('closeModal');
    }
  },
  beforeUpdate(){
    if(this.month == 2) {
      alert('2개월은 넘 적음');
      this.month = 3;
    }
  },
}
</script>

<style>

</style>
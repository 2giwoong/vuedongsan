<template>
  <div>
    <img :src="oneroom.image" alt="" class="room-img"><!--속성을 변경할때는 옆에 : 이 들어가야함-->
    <!-- <h4 @click="modal = true; clickContent = i">{{ onerooms[i].title }}</h4> -->
    <!--<h4 @click="$emit('openModal', oneroom.id)">{{ oneroom.title }}</h4> 부모에게 메세지 보낼떈 $emit(작명, 데이터) , 부모가 자식이 보낸 데이터를 볼때는 $event-->
    <h4 @click="send">{{ oneroom.title }}</h4>
    <p>{{ oneroom.price }}원</p>
  </div>
</template>

<script>
export default {
  name : 'cardComponent',
  props : {
    oneroom: Object,
    onerooms: Array,
    clickContent: Number,
    modal: Boolean,
  },
  data() {

  },
  methods : {
    send() {
      this.$emit('openModal', this.oneroom.id); //$emit 함수에선 this를 붙여야 가져와짐
    }
  }
}
</script>

<style>

</style>
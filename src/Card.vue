<template>
<!-- 상품 -->
  <div>
    <img :src="원룸.image" class="room-img">
    <h4 @click="send">상품명 : {{ 원룸.title }}</h4>
    <p>가격 : {{ 원룸.price }}원</p>
  </div>
</template>

<script>
export default {
  props: {
    원룸 : Object,
  },
  methods: {
    send(){
     this.$emit('openModal', this.원룸.id)
    }
  }
}
</script>

<style scoped>
</style>
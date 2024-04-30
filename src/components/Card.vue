<template>
  <div :class="['card', { 'is-fliped': food.fliped }]">
    <span class="card-icon">
      <transition name="flip">
        <div v-bind:key="food.fliped">
          {{ food.fliped ? food.icon : "" }}
        </div>
      </transition>
    </span>
  </div>
</template>
<script>
export default {
  props: ["food"],
};
</script>
<style>
.card {
  width: 65px;
  height: 65px;
  border-radius: 20px;
  background-color: darkgray;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.is-fliped {
    background-color: #fff;
}
.card-icon {
  font-size: 55px;
}
.flip-enter-active {
  transition: all 1s ease;
}

.flip-leave-active {
  display: none;
}

.flip-enter,
.flip-leave {
  transform: rotateY(180deg);
  opacity: 0;
}
</style>
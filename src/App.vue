<template>
  <div>
    <transition name="fade">
      <router-view/>
    </transition>
  </div>
</template>

<script>
export default{
  name : 'App'
}
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
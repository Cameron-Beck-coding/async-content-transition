<template>
  <transition name="fade" mode="out-in" class="transition">
    <div v-if="!loaded && showSpinner" key="async-content-spinner" name="loading-content">
      <div class="loading-content-div">
        <div class="spinner"></div>
      </div>
    </div>
    <div v-else-if="loaded" key="async-content-slot-container">
      <slot> </slot>
    </div>
  </transition>
</template>
<style>
loading-content-div {
  width: 100%;
  height: 100%;
}
.spinner {
  width: 40px;
  height: 40px;
  margin: 100px auto;
  background-color: #333;
  border-radius: 100%;
  -webkit-animation: sk-scaleout 1s infinite ease-in-out;
  animation: sk-scaleout 1s infinite ease-in-out;
}

@-webkit-keyframes sk-scaleout {
  0% {
    -webkit-transform: scale(0);
  }
  100% {
    -webkit-transform: scale(1);
    opacity: 0;
  }
}

@keyframes sk-scaleout {
  0% {
    -webkit-transform: scale(0);
    transform: scale(0);
  }
  100% {
    -webkit-transform: scale(1);
    transform: scale(1);
    opacity: 0;
  }
}
</style>
<script>
export default {
  props: {
    loaded: undefined,
    showSpinner: {
      default: true,
    },
  },
  mounted:()=>{
    const transition=document.querySelector('.transition')
    transition.addEventListener('transitionend',()=>{
      this.$emit('done')
    })
  },
  beforeDestroy(){
    window.removeEventListener('transitionend');
  }
  
};
</script>

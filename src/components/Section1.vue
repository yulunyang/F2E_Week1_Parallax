<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <section class="Section1 py-6 px-4 overflow-hidden">
    <div class="Section1-content proj-container mx-auto">
      <div class="flex justify-between text-white text-2xl xl:text-3xl">
        <div>I-    00</div>
        <div>HI- 99999</div>
        <div>Hex School</div>
      </div>
      <div class="py-28 xl:py-32 px-10 md:px-16 xl:px-0">
        <img src="@/assets/img/banner_LOGO1.png" alt="" class="object-contain block mx-auto">
      </div>
      <div class="flex justify-center flex-col items-center mb-48 xl:mb-36">
        <div class="text-3xl xl:text-4xl">
          <div class="flex items-center mb-5 cursor-pointer" @mouseover="mouseover(true)">
            <div class="mr-5" >
              <img src="@/assets/img/hammer.gif" alt="" class="hammer object-contain block mx-auto opacity-0" :class="{ 'opacity-100': isLogin }">
            </div>
            <a href="https://2022.thef2e.com/login" class="text-white" :class="{ 'proj-text-primary neon-effect': isLogin }" >1  LOG IN</a>
          </div>
          <div class="flex items-center cursor-pointer" @mouseover="mouseover(false)">
            <div class="mr-5">
              <img src="@/assets/img/hammer.gif" alt="" class="hammer object-contain block mx-auto opacity-0" :class="{ 'opacity-100': !isLogin }">
            </div>
            <a href="https://2022.thef2e.com/signup" class="text-white" :class="{ 'proj-text-primary neon-effect': !isLogin }">2  SIGN UP</a>
          </div>
        </div>
      </div>
      <div class="text-white text-2xl md:text-3xl lg:text-4xl">
        <p>INTERACTIVE AND RESPONSIVE WEB DESIGN.</p>
      </div>
    </div>
  </section>
</template>

<script>
import { gsap, ScrollTrigger, Draggable, MotionPathPlugin, TextPlugin } from 'gsap/all'
gsap.registerPlugin(gsap, ScrollTrigger, Draggable, MotionPathPlugin, TextPlugin )
import { onMounted, ref, onBeforeMount } from 'vue'
import { useStore } from "vuex"
export default {
  setup () {
    const store = useStore()
    const isLogin = ref(true)

    onBeforeMount(() => {
      window.addEventListener('keydown', handleKeyDown)
    })

    onMounted(()=> {
      !store.state.isLoading ? setGSAP() : null
    })

    const setGSAP = () => {
      gsap.from(".Section1-content", { y: 1000, duration: 5, delay: 1 })
    }

    const handleKeyDown = (event) => {
      event.preventDefault()
      if (event.keyCode === 38 || event.keyCode === 40) {
        isLogin.value = !isLogin.value
      } else if (event.keyCode === 13) {
        let url = isLogin.value ? 'https://2022.thef2e.com/login' : 'https://2022.thef2e.com/signup'
        window.open(url, '_blank')
      }
    }
    const mouseover = (val) => {
      isLogin.value = val
    }
    return {
      setGSAP, isLogin, handleKeyDown, mouseover, store
    }
  }
}
</script>

<style scoped lang="scss">
.Section1 {
  min-height: calc(100vh - 56px);
}

.centered{
  position:absolute;
  left:50%;
  top:50%;
  transform:translate(-50%,-50%);
}

.neon-effect {
  color:#fff;
  animation: neon-shine 7s infinite;
}

@keyframes neon-shine{

    0%{
      color: #B82A06;
    }

    80% {
      color: #B82A06;
    }
    90% {
      color: white;
    }
    100%{
      color: white;
    }

}

.hammer {
  width: 86px;
  height: 53px;
}
</style>

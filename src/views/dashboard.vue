<template>
  <div class="user_container">
    <div class="user_container_tabs">
      <div
          v-for="(tab, index) in tabs"
          :key="index"
          class="user_container_tabs"
          @click="changeTab(index)"
      >{{ tab }}</div>
    </div>
    <div class="user_container_pane">
      <transition name="slide-fade" >
        <keep-alive>
          <component :is="currentComponent"></component>
        </keep-alive>
      </transition>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import A from "@/components/settings/a.vue";
import B from "@/components/settings/b.vue";
import C from "@/components/settings/c.vue";

const currentComponent = ref(A);
const tabs = ['aaaa', 'bbbb', 'cccc'];

function changeTab(index) {
  if (index === 0) currentComponent.value = A;
  else if (index === 1) currentComponent.value = B;
  else if (index === 2) currentComponent.value = C;
}
</script>

<style scoped>
.user_container{
  width: 100%;
  display: flex;
  flex-direction: column;
}
.user_container_tabs{
  width: 100%;
  height: 50px;
  border: 1px solid #5900f8;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.user_container_tabs{
  width: 100px;
  height: 50px;
  background: #c2c2c4;
  display: flex;
  justify-content: center;
  align-items: center;
}
.user_container_pane{
  width: 100%;
  height: 100%;
  border: 1px solid #2ed91b;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative; /* 添加相对定位 */
  z-index: -1;
}
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.7s ease;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.slide-fade-enter-from {
  transform: translateX(100%);
  opacity: 0;
}

.slide-fade-enter-to {
  transform: translateX(0);
  opacity: 1;
}

.slide-fade-leave-from {
  transform: translateX(0);
  opacity: 1;
}

.slide-fade-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}
</style>

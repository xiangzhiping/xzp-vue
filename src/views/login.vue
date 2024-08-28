<template>
  <div class="login_container">
    <div class="login_container_header">XIANGZHIPING</div>
    <div class="login_container_pane">
      <transition :name="transitionName">
        <keep-alive>
          <component :is="currentComponent"></component>
        </keep-alive>
      </transition>
    </div>
    <div class="login_container_footer">
      <div
          v-for="(tab, index) in tabs"
          :key="index"
          class="login_container_tab"
          :class="{ active: index === currentIndex }"
      >
        <div class="login_container_icon" @click="changeTab(index)">
          <el-icon :size="22">
            <component :is="tab.icon" class="route_icon"/>
          </el-icon>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref, computed} from "vue";
import {Odometer, User, Lock, Key, Setting, Message} from '@element-plus/icons-vue'
import AccountPasswordLogin from '@/components/login/account_password_login.vue';
import CaptchaLogin from '@/components/login/captcha_login.vue';
import ForgetPassword from "@/components/login/forget_password.vue";
import Register from "@/components/login/register_account.vue";

const currentComponent = ref(AccountPasswordLogin);
const tabs = [
  {name: '账号密码登录', icon: User},
  {name: '验证码登录', icon: Message},
  {name: '忘记密码', icon: Lock},
  {name: '注册账号', icon: Key}
];
const currentIndex = ref(0);
const previousIndex = ref(currentIndex.value);
const transitionName = computed(() => {
  return currentIndex.value < previousIndex.value ? 'slide-fade-right' : 'slide-fade-left';
});


const changeTab = async (index) => {
  previousIndex.value = currentIndex.value;
  currentIndex.value = index;
  switch (index) {
    case 0:
      currentComponent.value = AccountPasswordLogin;
      break
    case 1:
      currentComponent.value = CaptchaLogin;
      break
    case 2:
      currentComponent.value = ForgetPassword;
      break
    case 3:
      currentComponent.value = Register;
  }
}
</script>

<style scoped>
.login_container {
  width: 500px;
  height: 400px;
  border-radius: 7px;
  border-bottom: 1px solid var(--el-border-color);
  box-shadow: var(--el-box-shadow-lighter);
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.login_container_header {
  width: 100%;
  height: 50px;
  color: #909399;
  font-size: 25px;
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
}

.login_container_footer {
  width: 100%;
  height: 50px;
  background: #c5ddfa;
  border-bottom: 1px solid var(--el-border-color);
  display: flex;
  justify-content: center;
  align-items: center;
}

.login_container_icon {
  width: 35px;
  height: 35px;
  border-radius: 50%;
  background: #34fd2d;
  display: flex;
  justify-content: center;
  align-items: center;
}

.login_container_tab {
  width: 125px;
  height: 50px;
  cursor: pointer;
  display: flex;
  color: #909399;
  justify-content: center;
  align-items: center;
}

.login_container_tab.active {
  background: #ffffff;
  color: #409EFF;
}

.login_container_pane {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.slide-fade-left-enter-active,
.slide-fade-left-leave-active,
.slide-fade-right-enter-active,
.slide-fade-right-leave-active {
  transition: all 0.5s ease;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.slide-fade-left-enter-from {
  transform: translateX(-100%);
}

.slide-fade-left-enter-to {
  transform: translateX(0);
}

.slide-fade-left-leave-from {
  transform: translateX(0);
}

.slide-fade-left-leave-to {
  transform: translateX(100%);
}

.slide-fade-right-enter-from {
  transform: translateX(100%);
}

.slide-fade-right-enter-to {
  transform: translateX(0);
}

.slide-fade-right-leave-from {
  transform: translateX(0);
}

.slide-fade-right-leave-to {
  transform: translateX(-100%);
}

</style>

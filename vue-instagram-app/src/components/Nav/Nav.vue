<script setup lang="ts">
import Container from '../UI/container.vue';
import AuthModal from '../AuthModal/AuthModal.vue';
import { RouterLink, useRouter } from 'vue-router';
import { AuthType } from '@/types';
import { useUserStore } from '@/stores/user';
import { storeToRefs } from 'pinia';

const router = useRouter();
const userStore = useUserStore();
const { user, loadingUser } = storeToRefs(userStore);
const { handleLogout } = userStore;
</script>

<template>
  <ALayoutHeader theme="light">
    <Container :styles="{}">
      <div class="nav">
        <RouterLink to="/"> Instagroom </RouterLink>
        <div v-if="!loadingUser" class="content">
          <div v-if="user" class="auth-btns">
            <a-button
              class="btn"
              type="primary"
              @click="router.push(`/${user.username}`)"
              >Profile</a-button
            >
            <a-button class="btn" type="primary" @click="handleLogout"
              >Signout</a-button
            >
          </div>
          <div v-else class="auth-btns">
            <AuthModal :type="AuthType.LOGIN" />
            <AuthModal :type="AuthType.SIGNIN" />
          </div>
        </div>
      </div>
    </Container>
  </ALayoutHeader>
</template>

<style scoped>
.nav {
  display: flex;
  justify-content: space-between;
}

.auth-btns {
  display: flex;
  align-items: center;
}

button {
  margin-right: 10px;
}

.content {
  display: flex;
  align-items: center;
}
</style>

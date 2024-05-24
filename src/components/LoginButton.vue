<template>
  <button class="login-button" @click="handleLoginClick">
    {{ isLoggedIn ? "ログアウト" : "ログイン" }}
  </button>
</template>

<script>
import { useAuth } from "./AuthContext.vue"

export default {
  name: "LoginButton",
  setup() {
    const { isLoggedIn, handleLoginClick } = useAuth();

    return {
      isLoggedIn,
      handleLoginClick,
    };
  }
}
</script>

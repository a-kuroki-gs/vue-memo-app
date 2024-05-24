<template>
  <slot />
</template>

<script>
import { ref, provide, inject } from "vue";

const AuthSymbol = Symbol();

export function useAuth() {
  const context = inject(AuthSymbol);
  if (!context) {
    throw new Error("useAuth must be used within an AuthProvider");
  }

  return context;
}

export default {
  name: "AuthProvider",
  setup() {
    const isLoggedIn = ref(false);

    const handleLoginClick = () => {
      isLoggedIn.value = !isLoggedIn.value;
    };

    provide(AuthSymbol, {
      isLoggedIn,
      handleLoginClick,
    });
  },
};
</script>

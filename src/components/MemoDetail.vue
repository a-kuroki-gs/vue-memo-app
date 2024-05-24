<template>
  <div>
    <h2>詳細</h2>
    <textarea
      rows="20"
      cols="40"
      v-model="text"
    ></textarea>
    <p></p>
      <div>
        <button
          v-if="isLoggedIn"
          class="custom-button"
          @click="$emit('edit-click', { ...memo, text })"
        >
          編集
        </button>
        <button
          v-if="isLoggedIn"
          class="custom-button"
          @click="$emit('delete-click', memo.id)"
        >
          削除
        </button>
      </div>
  </div>
</template>

<script>
import { ref, watch } from "vue";
import { useAuth } from "./AuthContext";

export default {
  name: "MemoDetail",
  props: {
    memo: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    const text = ref(props.memo.text);
    const { isLoggedIn } = useAuth();

    watch(() => props.memo.text, (newText) => {
      text.value = newText;
    });

    return {
      text,
      isLoggedIn,
    };
  }}
</script>

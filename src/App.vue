<template>
  <AuthProvider>
    <div class="header">
      <h1>メモアプリ</h1>
      <LoginButton />
    </div>
    <MemoContainer
      :memos="memos"
      :handleMemoClick="handleMemoClick"
      :handleNewMemo="handleNewMemo"
      :handleEditMemo="handleEditMemo"
      :handleDeleteMemo="handleDeleteMemo"
      :selectedMemo="selectedMemo"
    ></MemoContainer>
  </AuthProvider>
</template>

<script>
import MemoContainer from "./components/MemoContainer.vue"
import AuthProvider from "./components/AuthContext.vue"
import LoginButton from "./components/LoginButton.vue";
import { ref, onMounted, watch } from "vue";
import "./assets/App.css";

export default {
  name: "App",
  components: {
    MemoContainer,
    AuthProvider,
    LoginButton,
  },
  setup() {
    const memos = ref([]);
    const selectedMemo = ref(null);

    function saveToLocalStorage(memos) {
      localStorage.setItem("memos", JSON.stringify(memos));
    }

    onMounted(() => {
      const storedMemos = localStorage.getItem("memos");
      memos.value = storedMemos ? JSON.parse(storedMemos) : [];
    });

    watch(memos, (newMemos) => {
      saveToLocalStorage(newMemos);
    }, { deep: true });

    function handleMemoClick(memo) {
      selectedMemo.value = memo;
    }

    function handleNewMemo() {
      const maxId = Math.max(...memos.value.map((memo) => memo.id), 0);
      const newMemo = {
        id: maxId + 1,
        text: "新規メモ",
      };
      memos.value.push(newMemo);
      selectedMemo.value = newMemo;
    }

    function handleEditMemo(editedMemo) {
      memos.value = memos.value.map((memo) => {
        if (memo.id === editedMemo.id) {
          return editedMemo;
        } else {
          return memo;
        }
      });
      selectedMemo.value = editedMemo;
    }

    function handleDeleteMemo(memoId) {
      memos.value = memos.value.filter((memo) => memo.id !== memoId);
      selectedMemo.value = null;
    }

    return {
      memos,
      selectedMemo,
      handleMemoClick,
      handleNewMemo,
      handleEditMemo,
      handleDeleteMemo,
    };
  },
};
</script>

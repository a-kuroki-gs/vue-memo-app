<template>
  <div class="container">
    <div class="memo-list">
      <MemoList :memos="memos" @memo-click="handleMemoClick" />
      <button v-if="isLoggedIn" class="plus-button" @click="handleNewMemo">
        +
      </button>
    </div>
    <div class="memo-detail">
      <MemoDetail
        v-if="selectedMemo"
        :memo="selectedMemo"
        @edit-click="handleEditMemo"
        @delete-click="handleDeleteMemo"
      />
    </div>
  </div>
</template>

<script>
import MemoList from "./MemoList.vue"
import MemoDetail from "./MemoDetail.vue"
import { useAuth } from "./AuthContext"

export default {
  name: "MemoContainer",
  components: {
    MemoList,
    MemoDetail,
  },
  props: {
    memos: {
      type: Array,
      required: true,
    },
    handleMemoClick: {
      type: Function,
      required: true,
    },
    handleNewMemo: {
      type: Function,
      required: true,
    },
    handleEditMemo: {
      type: Function,
      required: true,
    },
    handleDeleteMemo: {
      type: Function,
      required: true,
    },
    selectedMemo: {
      type: Object,
    },
  },
  setup() {
    const { isLoggedIn } = useAuth();

    return {
      isLoggedIn,
    };
  }
}
</script>

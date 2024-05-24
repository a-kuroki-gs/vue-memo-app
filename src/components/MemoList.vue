<template>
  <div>
    <h2>一覧</h2>
    <ul>
      <li
        v-for="memo in memos"
        :key="memo.id"
        class="memo-item"
        @click="$emit('memo-click', memo)"
      >
        {{memo.text.split(/\n/)[0]}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MemoList",
  props: {
    memos: {
      type: Array,
      required: true,
    },
  },
}
</script>

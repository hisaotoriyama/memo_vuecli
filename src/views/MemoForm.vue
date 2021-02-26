<template>
  <div class="Edit">
    <h1>編集</h1>
    <textarea class="edit-text" placeholder="Memoを入力" v-model="selectedMemo" rows="3" cols="70"></textarea>
    <button class="btn" v-on:click = "editMemo(selectedMemo, selectedMemoIdx)" >編集</button>
    <button class="btn" v-on:click = "deleteMemo(selectedMemoIdx)" >削除</button>
  </div>
</template>

<script>
export default {
  props: ["editMemoList"],
  data: function() {
    return {
      selectedMemo:this.editMemoList.memo,
      selectedMemoIdx:this.editMemoList.idx
    }
  },
  methods: {
    editMemo: function(selectedMemo, selectedMemoIdx) {
      this.$emit("registerEdit", selectedMemo, selectedMemoIdx)
    },
    deleteMemo: function(selectedMemo, selectedMemoIdx) {
      this.$emit("registerDelete", selectedMemo, selectedMemoIdx)
    },
  }
}
</script>

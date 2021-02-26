<template>
  <div class="MemoList">
  <h1>メモリスト</h1>
   <ul>
    <li v-for="(eachMemo, idx) in allMemos" v-bind:key="idx" ><a href='#' v-on:click="editMemo(eachMemo, idx)">{{eachMemo.split("\n")[0]}}</a></li>
   </ul>
  </div>
</template>

<script>
export default {
  props: ["memoLists"],
  data: function() {
    return {
      allMemos:this.memoLists
    }
  },
  methods:{
    editMemo: function(eachMemo, idx) {
      this.$emit("showEditTable", eachMemo, idx)
    }
  }
}
</script>

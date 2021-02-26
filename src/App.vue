<template>
  <div class="container">
    <div class="item">
      <memo-list v-bind:memoLists="memos" v-on:showEditTable="showMemoForm"></memo-list>
    </div>
    <div class="item"><button class="btn" v-on:click="addNewMemo">+</button></div>

    <div class="item">
      <div v-if="show">
        <memo-form v-bind:editMemoList="editMemo" v-on:registerEdit="processEdit" v-on:registerDelete="processDelete"></memo-form>
      </div>
    </div>
  </div>
</template>

<script>
import MemoList from './views/MemoList.vue'
import MemoForm from './views/MemoForm.vue'

export default {
  components: {
    MemoList,
    MemoForm
  },
  data: function() {
    return {
      memos:[],
      show:false,
      editMemo:{},
      totalIdx:""
    }
  },
  methods: {
    loadMemos: function() {
      const jsonAllMemos = localStorage.getItem('memoList');
      const parsedJsonAllMemos = JSON.parse(jsonAllMemos);
      this.totalIdx = parsedJsonAllMemos.length;
      return parsedJsonAllMemos
    },
    setMemosAndReload: function() {
      localStorage.setItem('memoList', JSON.stringify(this.memos));
      this.memos = this.loadMemos();
      location.reload();
    },
    showMemoForm: function(eachMemo, idx) {
      this.show = true;
      this.editMemo = { memo: eachMemo, idx: idx };
    },
    addNewMemo: function() {
      this.show = true;
      this.editMemo = { memo: "", idx: this.totalIdx };
    },
    processEdit: function(selectedMemo, selectedMemoId) {
      this.memos[selectedMemoId] = selectedMemo;
      this.setMemosAndReload();
      this.show = false;
    },
    processDelete: function(selectedMemoId) {
      this.memos.splice(selectedMemoId,1);
      this.setMemosAndReload();
      this.show = false;
    }
  },
  created: function() {
    this.memos = this.loadMemos();
  },
}
</script>

<style>
.container {
  width: 550px;
  background-color: azure;
  border: solid;
  border-radius: 10px;
  border-color: lightskyblue;
  padding: 10px;
}

h1 {
  width: 500px;
  font-size: 20px;
  padding-left: 20px;
  border-radius: 5px;
  color: white;
  background-color: skyblue; 
}
.edit-text {
  margin-left: 20px;
  color: blue;
}

.btn {
  margin-left: 20px;
  font-size: 15px;
  color: blue;
}
</style>

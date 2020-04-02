<template>
  <div id ="myapp">
    <h1>ログイン後</h1>
    <button @click="logout">ログアウト</button>
    <button class="saveMemosBtn" @click="saveMemos">メモの保存</button>
    {{ myapp }}
  </div>
</template>>
<script>
export default {
  name: "myapp",
  props: ["user"],
  data(){
    return{
      myapp: null
    }
  },
  created: function() {
    firebase
      .firestore()
      .collection("myapp")
      .doc(this.user.uid)
      .get()
      .then(doc => {
      if (doc.exists && doc.data().myapp) {
        this.myapp = doc.data().myapp;
      }
    });
  },
  methods:{
    logout:function(){
      firebase.auth().signOut()
    },
    saveMemos: function() {
      firebase
        .firestore()
        .collection("myapp")
        .doc(this.user.uid)
        .set({ myapp: "テストデータだよ" });
    },
  }
}
</script>
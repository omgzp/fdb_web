<template>
  <div class="home">

    <!--<input type="file" accept=".fdb" id="fileId"/>-->
    <input type="text" v-model="fdbUrl" />
    <button @click="getSend()" > get发送</button>
    <button @click="postSend()" > post发送</button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      fdbUrl:""
    }
  },
  methods:{
      getSend(){
         /* var fdbfile  = document.querySelector("#fileId");
          alert(this.getPath(fdbfile));
          for(var item in fdbfile){
              console.log(fdbfile[item],item)
          }*/
         var that = this;
         if(that.fdbUrl!=""){
           this.$http.get(fdb_url+'/fdb',{
               params:{"url1":that.fdbUrl}
           }).then(function (res) {
              console.log(res);
            })
         }

      },
      postSend(){
        var that = this;
        if(that.fdbUrl!=""){
          this.$http.post(fdb_url+'/fdb',{
            "url1":that.fdbUrl
          }).then(function (res) {
            console.log(res);
          })
        }

      },
      getPath(obj) {
          if (obj) {
            if (window.navigator.userAgent.indexOf("MSIE") >= 1) {
              obj.select(); return document.selection.createRange().text;
            }
            else if (window.navigator.userAgent.indexOf("Firefox") >= 1) {
              if (obj.files) {
                return obj.files.item(0).getAsDataURL();
              }
              return obj.value;
            }
            return obj.value;
        }
      }
  }
}
</script>




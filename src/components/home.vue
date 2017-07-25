<template>
  <div class="home">
    <h1>批量发布fdb服务</h1>
    <!--<input type="file" accept=".fdb" id="fileId"/>-->
    <div>
      <label>項目名</label>
      <input type="text" v-model="projectName" />
    </div>
    <div>
      <label>文件路徑</label>
      <input type="text" v-model="fdbPath" />
    </div>
    <div>
      <button @click="getSend()" > get发送</button>
      <!--<button @click="postSend()" > post发送</button>-->
    </div>


  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      fdbPath:"",
      projectName:""
    }
  },
  methods:{
      getSend(){

        var that = this;
        var path  = that.fdbPath.replace(/\\/g, "/");
         if(that.fdbUrl!=""){
           this.$http.get(fdb_url+'/fdb/addDataSources',{
               params:{
                   "path":path,
                   "projectName":that.projectName
               }
           }).then(function (res) {
              console.log(res);
            })
         }


      },
      postSend(){
        var that = this;
        var path  = that.fdbPath.replace(/\\/g, "/");
        if(that.fdbUrl!=""){
          this.$http.post(fdb_url+'/fdb/addDataSources',{
            "path":path,
            "projectName":that.projectName
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




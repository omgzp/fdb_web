<template>
  <div class="home">
    <!--<h1>批量发布fdb服务</h1>
    &lt;!&ndash;<input type="file" accept=".fdb" id="fileId"/>&ndash;&gt;
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
    </div>-->

    <Row>
      <Col span="4" offset="10">
        <h1>批量发布fdb服务</h1>
      </Col>
      <Col span="4">
      <h3><a href="#/configFile">跳转设置页</a></h3>
      </Col>
    </Row>
    <Row>
      <Col span="2" offset="10">
          <label>項目名</label>

      </Col>
      <Col span="4">
        <input type="text" v-model="projectName" />
      </Col>
    </Row>
    <Row>
      <Col span="2" offset="10">
      <label>文件路徑</label>
      </Col>
      <Col span="4">
      <input type="text" v-model="fdbPath" />
      </Col>
    </Row>
    <Row>
      <Col span="2" offset="11">
      <Button type="info" @click="getSend()">发送</Button>
      </Col>

    </Row>
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




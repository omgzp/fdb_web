<template>
  <div class="configFile">
    <Row>
      <Col span="4" offset="10">
      <h1>批量生成配置文件</h1>
      </Col>
      <Col span="4">
      <h3><a href="#/">跳转发布服务页面</a></h3>
      </Col>
    </Row>
    <Row style="margin-top: 20px">
      <Col span="12" offset="6">
        <Table border :columns="columns4" :data="tableServers" @on-selection-change="checkChange"></Table>
      </Col>

    </Row>
    <Row>
      <Col span="2" offset="11">
      <Button type="info" @click="getFile()">生成配置文件</Button>
      </Col>

    </Row>
    <Row>
      <Col  offset="4">
      <label>配置信息</label>
      </Col>
      <Col span="16" offset="4">
      <Input class="textArea" rows="150" v-model="configData" type="textarea" :autosize="{minRows: 2,maxRows: 5}" placeholder="请输入..."></Input>
      </Col>

    </Row>
    <Row>
      <Col  offset="4">
      <label>图层信息</label>
      </Col>
      <Col span="16" offset="4">
      <Input class="textArea" rows="15" v-model="layerData" type="textarea" :autosize="{minRows: 2,maxRows: 5}" placeholder="请输入..."></Input>
      </Col>

    </Row>
  </div>
</template>

<script>
  export default {
      name:"configFile",
      data (){
          return {
            services:[
              {name:"",
                dataSet:[{
                  name:"",
                  featureClasses:[

                  ]
                }

              ]},
            ],
            columns4: [
              {
                type: 'selection',
                width: 60,
                align: 'center'
              },
              {
                title: '服务名',
                key: 'name'
              },

            ],
            servers: [],
            tableServers:[],
            configData:"",
            layerData:""
          }
      },
    methods:{
          getDatas(){
              var that = this;
            this.$http.get(fdb_url+'/fdb/getFdbList',{}).then(function (res) {
              var data = res.body;
              that.servers = [];
              that.tableServers=[];
              for(var i =0;i<data.length;i++){
                  var item={name:data[i],flag:false,index:i};
                  var tableItem={name:data[i],flag:false,index:i}
                  that.servers.push(item)
                  that.tableServers.push(tableItem);
              }
            })
          },
          checkChange(selection){
              for(let i = 0;i<this.servers.length;i++){
                this.servers[i].flag=false;
              }

              for(let i = 0;i<selection.length;i++){
                var index =selection[i].index;
                this.servers[index].flag=true;
              }
          },
          getFile(){
              var that = this;
              var datas = this.servers;
              var fdbservers = [];
              for(var i = 0;i<datas.length;i++){
                  if(datas[i].flag){
                    fdbservers.push(datas[i].name)
                  }
              }
              if(fdbservers.length==0){
                this.$Modal.error({
                  title: "错误提示",
                  content: '<p>未选中服务</p>'
                });
              }else{
                this.$http.post(fdb_url+'/fdb/getConfigFile',{
                  servers:fdbservers
                }).then(function (res) {
                    console.log("success");
                    var a = res.body;
                    console.log(res.body);
                    that.configData =JSON.stringify(res.body.configdata);
                    that.layerData = JSON.stringify(res.body.fdbdata)
                })
              }
          }
    },
    mounted(){
         this.getDatas();
    }
  }
</script>
<style scoped>
  .textArea{

  }
</style>

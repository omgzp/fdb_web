<template>
  <div class="configFile">
    <h1>批量生成配置文件</h1>
    <div>
      <button @click="getDatas()">获取数据</button>
    </div>
    <div>
      <ul>
        <li v-for="item in servers">
          {{item}}
        </li>
      </ul>
    </div>
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
            servers:["a","b"]

          }
      },
    methods:{
          getDatas(){
              var that = this;
            this.$http.get(fdb_url+'/fdb/getFdbList',{}).then(function (res) {
              console.log(res.body);
              that.servers = res.body;
            })
          }
    }
  }
</script>

<style lang="less">
    @import './donornow.less';
</style>

<template>
    <div class="donornow">
      <tlgy-header></tlgy-header>
        <el-container class="body">
          <el-main class="apptitle">
            <el-form ref="form"  label-width="150px">
              <el-form-item label="项目">
                <el-select v-model="form.project" placeholder="请选择" class="moveleft">
                    <el-option label="小明白血病" value="小明白血病"></el-option>
                    <el-option label="小红冠心病" value="小红冠心病"></el-option>
                    <el-option label="小黄眼角膜修复" value="小黄眼角膜修复"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="扫码捐款">
                <p><canvas id='qrimg' class="moveleft"></canvas></p>
              </el-form-item>
              <el-form-item label="链克地址">
                <el-input v-model="form.liankeaddress" :disabled="true" class="moveleft" style="width:400px;"></el-input>
              </el-form-item>
            </el-form>
          </el-main>
        </el-container>
      <tlgy-foot></tlgy-foot>
    </div>
</template>

<script>
import header from '../../common/header/header.vue'
import foot from '../../common/foot/foot.vue'

import Vue from 'vue'
import QRCode from 'qrcode'
import VueResource from 'vue-resource';

Vue.use(VueResource)
Vue.use(QRCode)

export default {
  data(){
    return{
       form: {
          project: '',
          liankeaddress: this.$store.state.bitaddress
        }
    }
  },
  components: {
    'tlgy-header': header,
    'tlgy-foot': foot
  },
   methods: {
    handleRemove(file, fileList) {
      console.log(file, fileList);
    }
  },
   mounted:function(){

        var posturl = "https://sandbox-walletapi.onethingpcs.com/api/linktest/tx_generate";
        var postdata = {
            email: "774392980@qq.com",
	        to: "0x5c949f437ef1cd1fe2f0d6268931ff3f29b04662",
	        value: "1000000000000000000",
	        callback: "www.baidu.com",
	        title: "transfer test",
	        desc: "to yiyanwannian",
        	tx_type: "tx_third",
	        sign: "ad3e466a20449e2318c50f94fb4954dc"
        };

        this.$http.post(
            posturl, 
            postdata, 
            {
                emulateJSON:true, 
                Host:"sandbox-walletapi.onethingpcs.com",
                }).then(
            function (res) {            
                                  // 处理成功的结果
                  alert(res.body.data.url);
              
            },function (err) {
                // 处理失败的结果
                alert("err");
            });

/*
        $http.post(posturl, postdata).success(function(response, status, headers, config){  
                if(response.status == 1){  
                    alert("修改成功！");  
                }  
            });
            */
/*
        alert("result.data.url");
        this.$http.interceptors.push(function(request) {
        request.method = 'POST';
        request.headers.set('Host', 'sandbox-walletapi.onethingpcs.com');
        request.headers.set('Content-Type', 'application/json;charset=utf-8');
      
       alert("result.data.url1");
        return function(response) {

            // modify response
            var result = response.body;
            alert("result.data.url1");

        }
    });
    */

/*
        var userbitaddress = this.$store.state.bitaddress;
          var canvas = document.getElementById('qrimg');
          
          QRCode.toCanvas(canvas, userbitaddress, function (error) {
          if (error) console.error(error)
            console.log('success!');
        });
        */
   }
}
</script>

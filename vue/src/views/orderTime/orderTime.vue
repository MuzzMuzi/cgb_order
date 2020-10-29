<template>
  <div class="app-container">
    <div class="filter-container">
      <el-form :rules="rules" ref="check" :model="check" label-width="150px"  style='margin-left:50px;'>
        <el-form-item label="选择时间" prop="orderTime">
          <el-date-picker
            value-format="yyyy-MM-dd HH:mm:ss"
            v-model="check.orderTime"
            type="datetime"
            placeholder="选择日期时间"
            default-time="12:00:00">
          </el-date-picker>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" icon="plus" size="mini" @click="checkTime('check')">检查
          </el-button>      
        </el-form-item>
      </el-form>
      <el-form v-loading="loading"  element-loading-text="后端休眠中" ref="form" :model="form" label-width="150px"  style='margin-left:50px;'>
        <el-form-item label="配送时间" prop="sendTime">
          <el-checkbox-group v-model="form.sendTime">
            <el-row>
              <el-checkbox :label="0" name="sendTime">00:00~00:30</el-checkbox>
              <el-checkbox :label="1" name="sendTime">00:30~01:00</el-checkbox>
              <el-checkbox :label="2" name="sendTime">01:00~01:30</el-checkbox>
              <el-checkbox :label="3" name="sendTime">01:30~02:00</el-checkbox>
              <el-checkbox :label="4" name="sendTime">02:00~02:30</el-checkbox>
              <el-checkbox :label="5" name="sendTime">02:30~03:00</el-checkbox>
            </el-row>
            <el-row>
              <el-checkbox :label="6" name="sendTime">03:00~03:30</el-checkbox>
              <el-checkbox :label="7" name="sendTime">03:30~04:00</el-checkbox>
              <el-checkbox :label="8" name="sendTime">04:00~04:30</el-checkbox>
              <el-checkbox :label="9" name="sendTime">04:30~05:00</el-checkbox>
              <el-checkbox :label="10" name="sendTime">05:00~05:30</el-checkbox>
              <el-checkbox :label="11" name="sendTime">05:30~06:00</el-checkbox>
            </el-row>
            <el-row>
              <el-checkbox :label="12" name="sendTime">06:00~06:30</el-checkbox>
              <el-checkbox :label="13" name="sendTime">06:30~07:00</el-checkbox>
              <el-checkbox :label="14" name="sendTime">07:00~07:30</el-checkbox>
              <el-checkbox :label="15" name="sendTime">07:30~08:00</el-checkbox>
              <el-checkbox :label="16" name="sendTime">08:00~08:30</el-checkbox>
              <el-checkbox :label="17" name="sendTime">08:30~09:00</el-checkbox>
            </el-row>
            <el-row>
              <el-checkbox :label="18" name="sendTime">09:00~09:30</el-checkbox>
              <el-checkbox :label="19" name="sendTime">09:30~10:00</el-checkbox>
              <el-checkbox :label="20" name="sendTime">10:00~10:30</el-checkbox>
              <el-checkbox :label="21" name="sendTime">10:30~11:00</el-checkbox>
              <el-checkbox :label="22" name="sendTime">11:00~11:30</el-checkbox>
              <el-checkbox :label="23" name="sendTime">11:30~12:00</el-checkbox>
            </el-row>
            <el-row>
              <el-checkbox :label="24" name="sendTime">12:00~12:30</el-checkbox>
              <el-checkbox :label="25" name="sendTime">12:30~13:00</el-checkbox>
              <el-checkbox :label="26" name="sendTime">13:00~13:30</el-checkbox>
              <el-checkbox :label="27" name="sendTime">13:30~14:00</el-checkbox>
              <el-checkbox :label="28" name="sendTime">14:00~14:30</el-checkbox>
              <el-checkbox :label="29" name="sendTime">14:30~15:00</el-checkbox>
            </el-row>
            <el-row>
              <el-checkbox :label="30" name="sendTime">15:00~15:30</el-checkbox>
              <el-checkbox :label="31" name="sendTime">15:30~16:00</el-checkbox>
              <el-checkbox :label="32" name="sendTime">16:00~16:30</el-checkbox>
              <el-checkbox :label="33" name="sendTime">16:30~17:00</el-checkbox>
              <el-checkbox :label="34" name="sendTime">17:00~17:30</el-checkbox>
              <el-checkbox :label="35" name="sendTime">17:30~18:00</el-checkbox>
            </el-row>
            <el-row>
              <el-checkbox :label="36" name="sendTime">18:00~18:30</el-checkbox>
              <el-checkbox :label="37" name="sendTime">18:30~19:00</el-checkbox>
              <el-checkbox :label="38" name="sendTime">19:00~19:30</el-checkbox>
              <el-checkbox :label="39" name="sendTime">19:30~20:00</el-checkbox>
              <el-checkbox :label="40" name="sendTime">20:00~20:30</el-checkbox>
              <el-checkbox :label="41" name="sendTime">20:30~21:00</el-checkbox>
            </el-row>
            <el-row>
              <el-checkbox :label="42" name="sendTime">21:00~21:30</el-checkbox>
              <el-checkbox :label="43" name="sendTime">21:30~22:00</el-checkbox>
              <el-checkbox :label="44" name="sendTime">22:00~22:30</el-checkbox>
              <el-checkbox :label="45" name="sendTime">22:30~23:00</el-checkbox>
              <el-checkbox :label="46" name="sendTime">23:00~23:30</el-checkbox>
              <el-checkbox :label="47" name="sendTime">23:30~23:59</el-checkbox>
            </el-row>
          </el-checkbox-group>
          <el-button type="primary" icon="plus" size="mini" @click="addTime()">确认</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        rules:{
          orderTime: [
            { required: true, message: '请输入时间', trigger: 'blur' }
          ]
        },
        check:{
          orderTime:''
        },
        form: {
          sendTime:[]
        },
        listLoading: false,//数据加载等待动画
        dialogStatus: 'create',
        dialogFormVisible: false,
        loading: true
      }
    },
    created() {
      this.doLoad()
    },
    methods: {
      doLoad(){
        this.api({
          url:"/user/doLoad",
          methods:"get"
        }).then(result => {
          this.loading=false
          this.form.sendTime=result
        })
      },  
      checkTime(check){
        this.$refs[check].validate(valid =>{
          if(valid){
            this.api({
              url: "/user/checkTime",
              method: "post",
              data: this.check
            }).then(data => {
                if(data){
                  this.$message({
                    message: "营业中!",
                    type: 'success'
                  });
                }else{
                  this.$message({
                    message: "不在营业时间内!",
                    type: 'warning'
                  });
                }       
              })
          }else{
            this.$message.error("还没有选择时间");
          }
        })
        
      },
      addTime(){
        this.api({
          url: "/user/addTime",
          method: "post",
          data: this.form
        }).then(data => {
          this.$message({
          message: "添加成功!",
          type: 'success'
        });
        })
      }
    }
  }
</script>

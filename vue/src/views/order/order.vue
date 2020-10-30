<template>
  <div class="app-container">
    <div class="filter-container">
      <el-form>
        <el-form-item>
          <el-button type="primary" icon="plus" @click="showCreate" v-if="hasPerm('order:add')">我要接单
          </el-button>
        </el-form-item>
      </el-form>
    </div>
    <el-table :data="list" v-loading.body="listLoading" element-loading-text="拼命加载中" border fit
              highlight-current-row>
      <el-table-column align="center" label="序号" width="80">
        <template slot-scope="scope">
          <span v-text="getIndex(scope.$index)"> </span>
        </template>
      </el-table-column>
      <el-table-column align="center" prop="orderId" label="订单号" style="width: 60px;"></el-table-column>
      <el-table-column align="center" prop="deliverymanId" label="配送员ID" style="width: 60px;"></el-table-column>
      <el-table-column align="center" prop="userId" label="客户ID" style="width: 60px;"></el-table-column>
      <el-table-column align="center" prop="totalPrice" label="总价" style="width: 60px;"></el-table-column>
      <el-table-column align="center" prop="remark" label="支付方式" style="width: 60px;"></el-table-column>
      <el-table-column align="center" prop="payMethod" label="订单状态" style="width: 60px;"></el-table-column>
      <el-table-column align="center" prop="createTime" label="订单创建时间" style="width: 60px;"></el-table-column>
      <el-table-column align="center" prop="updateTime" label="订单更新时间" style="width: 60px;"></el-table-column>
    </el-table>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        list: [],//表格的数据
        listLoading: false,//数据加载等待动画
        dialogStatus: 'create',
        dialogFormVisible: false
      }
    },
    created() {
      this.getList();
    },
    methods: {
      getList() {
        
      },
    }
  }
</script>

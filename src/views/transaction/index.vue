<template>
  <div class="uplink-container">
    <div style="color:#909399;margin-bottom: 30px">
      当前用户：{{ name }};
      用户角色: {{ userType }}
    </div>
    <div>
      <el-form ref="form" :model="tracedata" label-width="80px" size="mini" style="">
        <div>
          <el-form-item label="产品名称:" style="width: 300px" label-width="120px">
            <el-input v-model="tracedata.Farmer_input.Fa_fruitName" />
          </el-form-item>
          <el-form-item label="数量:" style="width: 300px" label-width="120px">
            <el-input v-model="tracedata.Farmer_input.Fa_origin" />
          </el-form-item>
        </div>
      </el-form>
      <span slot="footer" style="color: gray;" class="dialog-footer">
        <el-button v-show="userType != '消费者'" type="primary" plain style="margin-left: 220px;" @click="submittracedata()">发起交易申请</el-button>
      </span>
      <br>
      <br>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column label="用户" prop="traceability_code" />
        <el-table-column label="请求详情" prop="farmer_input.fa_fruitName" />
        <el-table-column label="操作" prop="farmer_input.fa_pickingTime">
          <template slot-scope="scope">
            <el-button type="primary" @click="agree(scope.$index, scope.row)">同意</el-button>
            <el-button type="danger" @click="reject(scope.$index, scope.row)">拒绝</el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Uplink',
  data() {
    return {
      tracedata: {
        traceability_code: '',
        Farmer_input: {
          Fa_fruitName: '',
          Fa_origin: '',
          Fa_plantTime: '',
          Fa_pickingTime: '',
          Fa_farmerName: ''
        },
        Factory_input: {
          Fac_productName: '',
          Fac_productionbatch: '',
          Fac_productionTime: '',
          Fac_factoryName: '',
          Fac_contactNumber: ''
        },
        Driver_input: {
          Dr_name: '',
          Dr_age: '',
          Dr_phone: '',
          Dr_carNumber: '',
          Dr_transport: ''
        },
        Shop_input: {
          Sh_storeTime: '',
          Sh_sellTime: '',
          Sh_shopName: '',
          Sh_shopAddress: '',
          Sh_shopPhone: ''
        }
      },
      loading: false,
      tableData: [
        {
          traceability_code: 'User1',
          farmer_input: {
            fa_fruitName: 'Apple',
            fa_pickingTime: '2022-01-01'
          }
        },
        {
          traceability_code: 'User2',
          farmer_input: {
            fa_fruitName: 'Banana',
            fa_pickingTime: '2022-01-02'
          }
        }
      ]
    }
  },
  computed: {
    ...mapGetters([
      'name',
      'userType'
    ])
  },
  methods: {
    submittracedata() {
      alert('提交成功!')
    }
  }
}

</script>

<style lang="scss" scoped>
.uplink {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>

<template>
  <div class="student">
    <el-table :data="tableData" stripe ali style="width: 100%">
      <el-table-column fixed type="index" label="章节" align="center" width="80">
      </el-table-column>
      <el-table-column prop="name" label="标题" align="center" width="250">
      </el-table-column>
      <el-table-column prop="province" label="作业状态" width="120">
        <template slot-scope="scope">
          <p class="status">
            <b class="submit" v-if="scope.row.province=='上海'"></b>
            <b class="submited" v-if="scope.row.province=='苏州'"></b>
            {{scope.row.province}}
          </p>
        </template>
      </el-table-column>
      <el-table-column prop="city" label="提交状况" align="center" width="120">
      </el-table-column>
      <el-table-column prop="address" label="平均分" align="center" width="300">
      </el-table-column>
      <el-table-column fixed="right" label="操作" align="center">
        <template slot-scope="scope">
          <el-button @click="exportExcel()" type="text" size="small">导出</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-button type="text" @click="importExcel()">导入表格</el-button>
    <excel-drag ref="excel" :show.sync="dialogVisible"></excel-drag>
  </div>
</template>

<script>
import excelDrag from "../components/dialog/ExcelDrag";
export default {
    name: "home",
    data() {
        return {
            tableData: [
                {
                    date: "2016-05-03",
                    name: "王小虎",
                    province: "上海",
                    city: "普陀区",
                    address: "上海市普陀区金沙江路 1518 弄",
                    zip: 200333
                },
                {
                    date: "2016-05-02",
                    name: "王小虎",
                    province: "上海",
                    city: "普陀区",
                    address: "上海市普陀区金沙江路 1518 弄",
                    zip: 200333
                },
                {
                    date: "2016-05-04",
                    name: "王小虎",
                    province: "上海",
                    city: "普陀区",
                    address: "上海市普陀区金沙江路 1518 弄",
                    zip: 200333
                },
                {
                    date: "2016-05-01",
                    name: "王小虎",
                    province: "上海",
                    city: "普陀区",
                    address: "上海市普陀区金沙江路 1518 弄",
                    zip: 200333
                }
            ],
            excelTitle: [
                "配件申请单号",
                "服务单",
                "申请类型",
                "需求日期",
                "收货人",
                "收货人电话",
                "审核状态"
            ],
            dialogVisible: false
        };
    },
    created() {
        this.init();
    },
    methods: {
        importExcel() {
            this.dialogVisible = true;
        },
        init: function() {},
        exportExcel() {
            this.jorce.exportExcel(
                "配件申请单",
                this.tableData,
                this.excelTitle
            );
        }
    },
    components: {
        excelDrag
    }
};
</script>
<style lang="scss">
.student {
    width: 80%;
    .el-table th {
        background-color: #f5f5f5;
        color: #b4bfc6;
    }
    .status {
        display: flex;
        align-items: center;
        letter-spacing: 0.5px;
        b {
            margin-right: 5px;
            width: 10px;
            height: 10px;
            border-radius: 50%;
        }
    }
}
.submit {
    background-color: red;
}
.submited {
    background-color: #7fd81e;
}
.wait {
    background-color: #ffd048;
}
.finish {
    background-color: #e2e2e2;
}
</style>

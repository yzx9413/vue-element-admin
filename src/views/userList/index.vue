<template>
  <div>
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column prop="username" label="用户名"></el-table-column>
      <el-table-column prop="profile" label="职位"></el-table-column>
      <el-table-column prop="create_time" label="创建时间"></el-table-column>
      <el-table-column prop="email" label="邮箱"></el-table-column>
      <el-table-column prop="phone" label="手机号码"></el-table-column>
    </el-table>
    <div class="block">
      <!-- <span class="demonstration">页数较少时的效果</span> -->
      <el-pagination
        background
        layout="prev, pager, next"
        :total="200"
        :page-size="10"
        @current-change="handleCurrentChange"
        :current-page.sync="currentPage"
      />
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "list",
  data() {
    return {
      tableData: [],
      currentPage: 1
    };
  },
  created() {
    axios.get("http://123.206.55.50:15000/users/list?page=1").then(res => {
      console.log(res.data.data);
      this.tableData = res.data.data.list;
    });
  },
  methods: {
    /** handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },*/
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      this.againRender(val);
    },
    againRender(val) {
      axios.get(`http://123.206.55.50:15000/users/list?page=${val}`).then(res => {
        console.log(res.data.data);
        this.tableData = res.data.data.list;
      });
    }
  }
};
</script>
<style scoped>
.block{
  width: 100%;
  text-align: center;
  margin-top: 5%;
}
</style>



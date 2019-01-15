<template>
  <div>
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column prop="username" label="用户名"></el-table-column>
      <el-table-column prop="profile" label="职位"></el-table-column>
      <el-table-column prop="create_time" label="创建时间"></el-table-column>
      <el-table-column prop="email" label="邮箱"></el-table-column>
      <el-table-column prop="phone" label="手机号码"></el-table-column>
      <el-table-column fixed="right" label="操作" width>
        <template slot-scope="scope">
          <el-button type="text" size="small" >查看</el-button>
          <el-button type="text" size="small" @click="open" >编辑</el-button>
        </template>
      </el-table-column>
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


    
    <!-- <el-dialog title="收货地址" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="活动名称" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="活动区域" :label-width="formLabelWidth">
          <el-select v-model="form.region" placeholder="请选择活动区域">
            <el-option label="区域一" value="shanghai"></el-option>
            <el-option label="区域二" value="beijing"></el-option>
          </el-select>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>-->
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "list",
  data() {
    return {
      tableData: [],
      currentPage: 1,
      checkArr:['codeing','UI','leader','Boss']
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
      axios
        .get(`http://123.206.55.50:15000/users/list?page=${val}`)
        .then(res => {
          console.log(res.data.data);
          this.tableData = res.data.data.list;
        });
    },
    open() {
        this.$alert(`<input type="checkbox" v-for="check in checkArr" :value="check">`, 'HTML 片段', {
          dangerouslyUseHTMLString: true
        });
    }
  }
};
</script>
<style scoped>
.block {
  width: 100%;
  text-align: center;
  margin-top: 1%;
}
</style>
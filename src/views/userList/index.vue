<template>
  <div>
    <!-- 表格 -->
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column prop="username" label="用户名"></el-table-column>
      <el-table-column prop="profile" label="职位"></el-table-column>
      <el-table-column prop="create_time" label="创建时间"></el-table-column>
      <el-table-column prop="email" label="邮箱"></el-table-column>
      <el-table-column prop="phone" label="手机号码"></el-table-column>
      <el-table-column fixed="right" label="操作" width>
        <template slot-scope="scope">
          <el-button type="text" size="small">查看</el-button>
          <el-button type="text" size="small" @click="dialogTableVisible = true">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>

    <!-- 分页 -->
    <div class="block">
      <el-pagination
        background
        layout="prev, pager, next"
        :total="200"
        :page-size="9"
        @current-change="handleCurrentChange"
        :current-page.sync="currentPage"
      />
    </div>

    <!-- 弹框 -->
    <el-dialog title="个人信息" :visible.sync="dialogTableVisible">
      <el-row>
        <el-col :span="6">
          <div class="grid-content bg-purple">用户名：</div>
        </el-col>
        <el-col :span="12">
          <div class="grid-content bg-purple-light">
            <el-input placeholder="请输入内容" clearable></el-input>
          </div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="6">
          <div class="grid-content bg-purple">职位：</div>
        </el-col>
        <el-col :span="12">
          <div class="grid-content bg-purple-light">
            <el-radio
              v-for="(check,ind) in checkArr"
              v-model="radio"
              :label="ind"
              :key="ind"
            >{{check}}</el-radio>
          </div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="6">
          <div class="grid-content bg-purple">邮箱：</div>
        </el-col>
        <el-col :span="12">
          <div class="grid-content bg-purple-light">
            <el-input placeholder="请输入内容" clearable></el-input>
          </div>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="6">
          <div class="grid-content bg-purple">手机号码：</div>
        </el-col>
        <el-col :span="12">
          <div class="grid-content bg-purple-light">
            <el-input placeholder="请输入内容" clearable></el-input>
          </div>
        </el-col>
      </el-row>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "list",
  data() {
    return {
      radio: "1",
      tableData: [],
      currentPage: 1,
      checkArr: ["codeing", "UI", "leader", "Boss"],
      dialogTableVisible: false,
      dialogFormVisible: false,
      formLabelWidth: "120px"
    };
  },
  created() {
    axios.get("http://123.206.55.50:15000/users/list?page=1").then(res => {
      console.log(res.data.data);
      this.tableData = res.data.data.list;
    });
  },
  methods: {
    handleCurrentChange(val) {
      // console.log(`当前页: ${val}`);
      this.againRender(val);
    },
    againRender(val) {
      axios
        .get(`http://123.206.55.50:15000/users/list?page=${val}`)
        .then(res => {
          console.log(res.data.data);
          this.tableData = res.data.data.list;
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
.el-table-column {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.el-row {
  text-align: center;
  line-height: 36px;
  margin-bottom: 3%;
}
.grid-content.bg-purple-light {
  display: flex;
}
.el-radio {
  line-height: 36px;
}
</style>
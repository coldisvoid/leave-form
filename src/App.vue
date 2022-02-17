<template>
  <div id="app">
        <span>输入姓名搜索</span>
        <el-input type="text" placeholder="请输入姓名的关键字进行查找" style="width: 40%" v-model="searchname">
      <el-button slot="append" icon="el-icon-search" @click="SearchEmps"></el-button>
    </el-input>
    <!-- Form -->
    <el-button @click="addDialogFormVisible = true">新建</el-button>

    <el-dialog title="新增请假单" :visible.sync="addDialogFormVisible" width="90%">
      <el-form :model="addDialogForm">
        <el-form-item label="请假人员" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="部门" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="办公地点" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="人员类别" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="入职时间" :label-width="formLabelWidth">
            <el-date-picker
              v-model="addDialogForm.hireDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
        </el-form-item>
        <el-form-item label="填写时间" :label-width="formLabelWidth">
            <el-date-picker
              v-model="addDialogForm.hireDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
        </el-form-item>
        <el-form-item label="请假类别	" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="职务	" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="出生年月" :label-width="formLabelWidth">
            <el-date-picker
              v-model="addDialogForm.hireDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
        </el-form-item>
        <el-form-item label="毕业时间" :label-width="formLabelWidth">
            <el-date-picker
              v-model="addDialogForm.hireDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
        </el-form-item>
        <el-form-item label="请假事由	" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="请假时间" :label-width="formLabelWidth">
            <el-date-picker
              v-model="addDialogForm.hireDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
        </el-form-item>
        <el-form-item label=" " :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label=" " :label-width="formLabelWidth">
            <el-date-picker
              v-model="addDialogForm.hireDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
        </el-form-item>
        <el-form-item label="	" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="天数" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="销假时间" :label-width="formLabelWidth">
            <el-date-picker
              v-model="addDialogForm.hireDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
        </el-form-item>
        <el-form-item label="	" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="天数" :label-width="formLabelWidth">
          <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
        </el-form-item>

      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submitAddDialogForm()"
          >确 定</el-button
        >
      </div>
    </el-dialog>

    <el-dialog title="更新请假单" :visible.sync="updateDialogFormVisible">
      <el-form :model="updateDialogForm">
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input
            v-model="updateDialogForm.name"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-form-item label="部门" :label-width="formLabelWidth">
          <el-input
            v-model="updateDialogForm.department"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-form-item label="入职日期" :label-width="formLabelWidth">
          <div class="block">
            <el-date-picker
              v-model="updateDialogForm.hireDate"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
          </div>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="updateDialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submitUpdateDialogForm()"
          >确 定</el-button
        >
      </div>
    </el-dialog>

    <!-- 列表 -->

    <el-table
      :data="leaveForms"
      :row-key="
        (row) => {
          return row.id;
        }
      "
      style="width: 100%"
    >
      <el-table-column prop="id" label="id" width="180"> </el-table-column>
      <el-table-column prop="name" label="姓名" width="180"> </el-table-column>
      <el-table-column prop="department" label="部门" width="180"> </el-table-column>
      <el-table-column prop="hireDate" label="入职日期" width="180"> </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
            >编辑</el-button
          >
          <el-button
            size="mini"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)"
            >删除</el-button
          >
        </template>
      </el-table-column>
    </el-table>
    <!-- 分页 -->
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="pagination.page"
        :page-sizes="[5, 10, 20, 50]"
        :page-size="pagination.size"
        layout="total, sizes, prev, pager, next, jumper"
        :total="pagination.count"
      >
      </el-pagination>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      //新增
      addDialogFormVisible: false,
      addDialogForm: {},
      formLabelWidth: "120px",
      //列表
      leaveForms: [],
      //修改
      updateDialogFormVisible: false,
      updateDialogForm: {},
      //分页
      pagination:{
        page:1,
        size:5,
        count:0
      },
      //查询
      searchname:""

    };
  },
  created() {
    this.getNewPage()
  },
  methods: {
    //
    getFormList() {
      this.getNewPage()
      // setTimeout(() => {
      //   this.$http
      //     .get("users")
      //     .then((response) => {
      //       this.leaveForms = response.data;
      //     })
      //     .catch((e) => {
      //       console.log(e);
      //     });
      // }, 250);
    },
    addForm(form) {
      this.$http
        .post("users", form)
        .then
        // response => {
        //   console.log(response)
        // }
        ()
        .catch((e) => {
          console.log(e);
        });
      this.getFormList();
    },

    handleEdit(index, row) {
      this.updateDialogForm = { ...this.leaveForms[index] };
      console.log("leaveForms", this.leaveForms, row);
      this.updateDialogFormVisible = true;
    },
    handleDelete(index, row) {
      console.log("Delete:", index, row.id);
      this.$http
        .delete("users/" + row.id)
        .then
        // response => {
        //   console.log(response)
        // }
        ()
        .catch((e) => {
          console.log(e);
        });
      this.getFormList();
    },
    submitAddDialogForm() {
      this.addForm(this.addDialogForm);
      this.dialogFormVisible = false;
    },
    submitUpdateDialogForm() {
      this.addForm(this.updateDialogForm);
      this.updateDialogFormVisible = false;
    },
    //分页
    handleSizeChange(val) {
      this.pagination.size=val
      this.pagination.page=1
      this.getNewPage()
    },
    handleCurrentChange(val) {
      this.pagination.page=val
      if(this.searchname!=""){
        this.SearchEmps()
        return
      }
      this.getNewPage()
    },
    getNewPage(){
      setTimeout(()=>{
        this.$http.get("users/" + this.pagination.page +"/"+this.pagination.size)
            .then((res) => {
              this.leaveForms = res.data.result;
              this.pagination.count = res.data.count;
          })
            .catch((e) => {
              console.log(e);
            });
      },250)

    } ,
    //查询
    SearchEmps(){
      if(this.searchname==""){
        this.getNewPage()
        return
      }
      setTimeout(()=>{
        this.$http.get("users/search/" + this.pagination.page +"/"+this.pagination.size+
        "/"+this.searchname)
            .then((res) => {
              this.leaveForms = res.data.result;
              this.pagination.count = res.data.count;
          })
            .catch((e) => {
              console.log(e);
            });
      },250)
    }
  }
}
</script>

<style>

</style>

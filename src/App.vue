<template>
  <div id="app">
    <span>输入姓名搜索</span>
    <el-input
      type="text"
      placeholder="请输入姓名的关键字进行查找"
      style="width: 40%"
      v-model="searchname"
    >
      <el-button
        slot="append"
        icon="el-icon-search"
        @click="SearchEmps"
      ></el-button>
    </el-input>
    <!-- Form -->
    <el-button @click="addDialogFormVisible = true">新建</el-button>

    <el-dialog
      title="新增请假单"
      :visible.sync="addDialogFormVisible"
      width="90%"
      top="5vh"
    >
      <el-form :model="addDialogForm" size="mini">
        <el-row>
          <el-col :span="12">
            <el-form-item
              label="请假人员"
              :label-width="formLabelWidth"
              size="small"
            >
              <el-input
                v-model="addDialogForm.name"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="填写时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="addDialogForm.writeDate"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker> </el-form-item
          ></el-col>
        </el-row>
        <el-row>
          <el-col :span="12"
            ><el-form-item label="部门" :label-width="formLabelWidth">
              <el-input
                v-model="addDialogForm.department"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="请假类别	" :label-width="formLabelWidth">
              <el-select v-model="addDialogForm.leaveType" placeholder="请选择">
                <el-option
                  v-for="item in leaveTypeOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select> </el-form-item
          ></el-col>
        </el-row>
        <el-row>
          <el-col :span="12"
            ><el-form-item label="办公地点" :label-width="formLabelWidth">
              <el-input
                v-model="addDialogForm.workLocation"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="职务	" :label-width="formLabelWidth">
              <el-input
                v-model="addDialogForm.job"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
        </el-row>
        <el-row>
          <el-col :span="12"
            ><el-form-item label="人员类别" :label-width="formLabelWidth">
              <el-input
                v-model="addDialogForm.memberType"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="出生年月" :label-width="formLabelWidth">
              <el-date-picker
                v-model="addDialogForm.birthDate"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker> </el-form-item
          ></el-col>
        </el-row>
        <el-row>
          <el-col :span="12"
            ><el-form-item label="入职时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="addDialogForm.hireDate"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="毕业时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="addDialogForm.graduation"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="请假事由	" :label-width="formLabelWidth">
          <el-input
            v-model="addDialogForm.reason"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-row>
          <el-col :span="5">
            <el-form-item label="请假时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="addDialogForm.leaveStart"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker>
            </el-form-item>
          </el-col>
          <el-col :span="4">
            <el-form-item label="" :label-width="formLabelWidth">
              <el-select
                v-model="addDialogForm.leaveStartPeriod"
                placeholder="请选择"
              >
                <el-option
                  v-for="item in PeriodOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select> </el-form-item
          ></el-col>
          <el-col :span="5">
            <el-form-item label="至" :label-width="formLabelWidth">
              <el-date-picker
                v-model="addDialogForm.leaveEnd"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker> </el-form-item
          ></el-col>
          <el-col :span="4">
            <el-form-item label="" :label-width="formLabelWidth">
              <el-select
                v-model="addDialogForm.leaveEndPeriod"
                placeholder="请选择"
              >
                <el-option
                  v-for="item in PeriodOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select> </el-form-item
          ></el-col>
          <el-col :span="4">
            <el-form-item label="天数" :label-width="formLabelWidth">
              <el-input
                v-model="addDialogForm.leaveTotal"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
        </el-row>

        <el-row>
          <el-col :span="5">
            <el-form-item label="销假时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="addDialogForm.returnToWork"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="	" :label-width="formLabelWidth">
              <el-select
                v-model="addDialogForm.returnPeriod"
                placeholder="请选择"
              >
                <el-option
                  v-for="item in PeriodOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="天数" :label-width="formLabelWidth">
              <el-input
                v-model="addDialogForm.returnTotal"
                autocomplete="off"
              ></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submitAddDialogForm()"
          >确 定</el-button
        >
      </div>
    </el-dialog>
    <el-dialog
      title="更新请假单"
      :visible.sync="updateDialogFormVisible"
      width="90%"
      top="5vh"
    >
      <el-form :model="updateDialogForm" size="mini">
        <el-row>
          <el-col :span="12">
            <el-form-item
              label="请假人员"
              :label-width="formLabelWidth"
              size="small"
            >
              <el-input
                v-model="updateDialogForm.name"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="填写时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="updateDialogForm.writeDate"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker> </el-form-item
          ></el-col>
        </el-row>
        <el-row>
          <el-col :span="12"
            ><el-form-item label="部门" :label-width="formLabelWidth">
              <el-input
                v-model="updateDialogForm.department"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="请假类别	" :label-width="formLabelWidth">
              <el-select v-model="updateDialogForm.leaveType" placeholder="请选择">
                <el-option
                  v-for="item in leaveTypeOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select> </el-form-item
          ></el-col>
        </el-row>
        <el-row>
          <el-col :span="12"
            ><el-form-item label="办公地点" :label-width="formLabelWidth">
              <el-input
                v-model="updateDialogForm.workLocation"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="职务	" :label-width="formLabelWidth">
              <el-input
                v-model="updateDialogForm.job"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
        </el-row>
        <el-row>
          <el-col :span="12"
            ><el-form-item label="人员类别" :label-width="formLabelWidth">
              <el-input
                v-model="updateDialogForm.memberType"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="出生年月" :label-width="formLabelWidth">
              <el-date-picker
                v-model="updateDialogForm.birthDate"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker> </el-form-item
          ></el-col>
        </el-row>
        <el-row>
          <el-col :span="12"
            ><el-form-item label="入职时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="updateDialogForm.hireDate"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker> </el-form-item
          ></el-col>
          <el-col :span="12">
            <el-form-item label="毕业时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="updateDialogForm.graduation"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="请假事由	" :label-width="formLabelWidth">
          <el-input
            v-model="updateDialogForm.reason"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-row>
          <el-col :span="5">
            <el-form-item label="请假时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="updateDialogForm.leaveStart"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker>
            </el-form-item>
          </el-col>
          <el-col :span="4">
            <el-form-item label="" :label-width="formLabelWidth">
              <el-select
                v-model="updateDialogForm.leaveStartPeriod"
                placeholder="请选择"
              >
                <el-option
                  v-for="item in PeriodOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select> </el-form-item
          ></el-col>
          <el-col :span="5">
            <el-form-item label="至" :label-width="formLabelWidth">
              <el-date-picker
                v-model="updateDialogForm.leaveEnd"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker> </el-form-item
          ></el-col>
          <el-col :span="4">
            <el-form-item label="" :label-width="formLabelWidth">
              <el-select
                v-model="updateDialogForm.leaveEndPeriod"
                placeholder="请选择"
              >
                <el-option
                  v-for="item in PeriodOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select> </el-form-item
          ></el-col>
          <el-col :span="4">
            <el-form-item label="天数" :label-width="formLabelWidth">
              <el-input
                v-model="updateDialogForm.leaveTotal"
                autocomplete="off"
              ></el-input> </el-form-item
          ></el-col>
        </el-row>

        <el-row>
          <el-col :span="5">
            <el-form-item label="销假时间" :label-width="formLabelWidth">
              <el-date-picker
                v-model="updateDialogForm.returnToWork"
                type="date"
                placeholder="选择日期"
              >
              </el-date-picker>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="	" :label-width="formLabelWidth">
              <el-select
                v-model="updateDialogForm.returnPeriod"
                placeholder="请选择"
              >
                <el-option
                  v-for="item in PeriodOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="天数" :label-width="formLabelWidth">
              <el-input
                v-model="updateDialogForm.returnTotal"
                autocomplete="off"
              ></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
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
      <el-table-column prop="department" label="部门" width="180">
      </el-table-column>
      <el-table-column prop="hireDate" label="入职日期" width="180">
      </el-table-column>
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
var dayjs = require("dayjs");
//import dayjs from 'dayjs' // ES 2015
dayjs().format();
export default {
  name: "App",

  data() {
    return {
      //新增
      addDialogFormVisible: false,
      addDialogForm: {
        leaveTotal: 0,
        leaveStart: null,
        leaveEnd: null,
        leaveStartPeriod:null,
        leaveEndPeriod:null,

      },
      formLabelWidth: "120px",
      //列表
      leaveForms: [],
      //修改
      updateDialogFormVisible: false,
      updateDialogForm: {},
      //分页
      pagination: {
        page: 1,
        size: 5,
        count: 0,
      },
      //查询
      searchname: "",
      //leaveType
      leaveTypeOptions: [
        {
          value: "病假",
          label: "病假",
        },
        {
          value: "事假",
          label: "事假",
        },
        {
          value: "年休假",
          label: "年休假",
        },
      ],
      PeriodOptions: [
        {
          value: "上午",
          label: "上午",
        },
        {
          value: "下午",
          label: "下午",
        },
      ],
    };
  },
  watch: {
    addDialogForm: {
      handler(val) {
          const start = dayjs(val.leaveStart);
          const end = dayjs(val.leaveEnd);
          if(!isNaN(end.diff(start,'day'))){
            let res=end.diff(start,'day')
            if(val.leaveStartPeriod=="下午"){
              res-=0.5
            }
            if(val.leaveEndPeriod=="上午"){
              res+=0.5
            }else if(val.leaveEndPeriod=="下午"){
              res+=1
            }
            val.leaveTotal=res
          }
          console.log("change",val)
      },
      immediate: true,
      deep: true, // 可以深度检测到 person 对象的属性值的变化
    },
    updateDialogForm: {
      handler(val) {
          const start = dayjs(val.leaveStart);
          const end = dayjs(val.leaveEnd);
          if(!isNaN(end.diff(start,'day'))){
            let res=end.diff(start,'day')
            if(val.leaveStartPeriod=="下午"){
              res-=0.5
            }
            if(val.leaveEndPeriod=="上午"){
              res+=0.5
            }else if(val.leaveEndPeriod=="下午"){
              res+=1
            }
            val.leaveTotal=res
          }
          console.log("change",val)
      },
      immediate: true,
      deep: true, // 可以深度检测到 person 对象的属性值的变化
    },
  },
  created() {
    this.getNewPage();
  },
  methods: {
    //
    getFormList() {
      this.getNewPage();
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
      this.pagination.size = val;
      this.pagination.page = 1;
      this.getNewPage();
    },
    handleCurrentChange(val) {
      this.pagination.page = val;
      if (this.searchname != "") {
        this.SearchEmps();
        return;
      }
      this.getNewPage();
    },
    getNewPage() {
      setTimeout(() => {
        this.$http
          .get("users/" + this.pagination.page + "/" + this.pagination.size)
          .then((res) => {
            this.leaveForms = res.data.result;
            this.pagination.count = res.data.count;
          })
          .catch((e) => {
            console.log(e);
          });
      }, 250);
    },
    //查询
    SearchEmps() {
      if (this.searchname == "") {
        this.getNewPage();
        return;
      }
      setTimeout(() => {
        this.$http
          .get(
            "users/search/" +
              this.pagination.page +
              "/" +
              this.pagination.size +
              "/" +
              this.searchname
          )
          .then((res) => {
            this.leaveForms = res.data.result;
            this.pagination.count = res.data.count;
          })
          .catch((e) => {
            console.log(e);
          });
      }, 250);
    },
  },
};
</script>

<style>
</style>

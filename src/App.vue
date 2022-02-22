<template>
  <div id="app">
    <!-- 查询输入框和按钮；创建按钮 -->
    <el-form :inline="true" :model="searchForm" class="demo-form-inline">
      <el-form-item label="姓名">
        <el-input
          v-model="searchForm.searchname"
          placeholder="请假人姓名"
        ></el-input>
      </el-form-item>
      <el-form-item label="请假类型">
        <el-select v-model="searchForm.leaveType" placeholder="请假类型">
          <el-option
            v-for="item in leaveTypeOptions"
            :label="item.lable"
            :key="item.lable"
            :value="item.value"
          ></el-option>
        </el-select>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="SearchEmps">查询</el-button>
      </el-form-item>
      <el-button type="primary" @click="addDialogFormVisible = true"
        >新建</el-button
      >
    </el-form>
    <!-- 新增请假单的用户输入表单 -->
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
        <el-form-item label="请假事由" :label-width="formLabelWidth">
          <el-input
            type="textarea"
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
                disabled
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
                disabled
                v-model="addDialogForm.returnTotal"
                autocomplete="off"
              ></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="addDialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submitAddDialogForm">确 定</el-button>
      </div>
    </el-dialog>
    <!-- 更新请假单的用户输入表单 -->
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
              <el-select
                v-model="updateDialogForm.leaveType"
                placeholder="请选择"
              >
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
            type="textarea"
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
                disabled
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
                disabled
                v-model="updateDialogForm.returnTotal"
                autocomplete="off"
              ></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="updateDialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submitUpdateDialogForm()"
          >确 定</el-button
        >
      </div>
    </el-dialog>
    <!-- 变更历史的展示列表 -->
    <el-dialog
      title="变更历史"
      width="90%"
      top="5vh"
      height="250"
      :visible.sync="historyDialogTableVisible"
    >
      <el-table :data="historyForms">
        <el-table-column
          property="id"
          label="记录编号"
          width="150"
        ></el-table-column>
        <el-table-column
          fixed
          :formatter="createTimeFormatter"
          property="createTime"
          label="提交时间"
        ></el-table-column>
        <el-table-column property="name" label="姓名"></el-table-column>
        <el-table-column
          prop="department"
          label="部门"
          width="180"
        ></el-table-column>
        <el-table-column prop="leaveType" label="请假类型" width="180">
        </el-table-column>
        <el-table-column property="reason" label="请假事由"></el-table-column>
      </el-table>
    </el-dialog>
    <!-- 请假单展示列表 -->
    <el-table
      height="500"
      :data="leaveForms"
      :row-key="
        (row) => {
          return row.id;
        }
      "
      style="width: 100%"
    >
      <el-table-column prop="id" label="记录编号"> </el-table-column>
      <el-table-column prop="name" label="姓名"> </el-table-column>
      <el-table-column prop="department" label="部门"> </el-table-column>
      <el-table-column prop="leaveType" label="请假类型"> </el-table-column>
      <el-table-column
        prop="reason"
        label="请假事由"
        min-width="180"
        show-overflow-tooltip
      >
      </el-table-column>
      <el-table-column label="操作" width="225" fixed="right">
        <template slot-scope="scope">
          <el-button-group>
            <el-button
              size="mini"
              type="primary"
              @click="handleEdit(scope.$index, scope.row)"
              >编辑</el-button
            >
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)"
              >删除</el-button
            >
            <el-button
              size="mini"
              type="info"
              @click="handleRecord(scope.$index, scope.row)"
              >历史变更</el-button
            >
          </el-button-group>
        </template>
      </el-table-column>
    </el-table>
    <!-- 分页控制 -->
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
//引入dayjs计算时间间隔
var dayjs = require("dayjs");
dayjs().format();

export default {
  name: "App",

  data() {
    return {
      //新增表单的数据
      addDialogFormVisible: false,
      addDialogForm: {
        leaveStart: null,
        leaveEnd: null,
        leaveStartPeriod: null,
        leaveEndPeriod: null,
        leaveTotal: null,
        returnToWork: null,
        returnPeriod: null,
        returnTotal: null,
      },
      formLabelWidth: "120px",
      //保存请假单展示列表
      leaveForms: [],
      //修改表单的数据
      updateDialogFormVisible: false,
      updateDialogForm: {
        leaveStart: null,
        leaveEnd: null,
        leaveStartPeriod: null,
        leaveEndPeriod: null,
        leaveTotal: null,
        returnToWork: null,
        returnPeriod: null,
        returnTotal: null,
      },
      //分页的参数
      pagination: {
        page: 1,//当前页码
        size: 5,//页大小
        count: 0,//记录总数
      },
      //查询用
      searchForm: {
        searchname: "",
        leaveType: "",
      },
      savedSearchForm: {
        searchname: "",
        leaveType: "",
      },
      //变更历史
      historyForms: [],
      historyDialogTableVisible: false,
      //leaveType选项
      leaveTypeOptions: [
        {
          value: "",
          label: "",
        },
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
        {
          value: "产假",
          label: "产假",
        },
        {
          value: "陪产假",
          label: "陪产假",
        },
        {
          value: "丧假",
          label: "丧假",
        },
        {
          value: "婚假",
          label: "婚假",
        },
        {
          value: "计生假",
          label: "计生假",
        },
        {
          value: "流产假",
          label: "流产假",
        },
        {
          value: "出差休假",
          label: "出差休假",
        },
        {
          value: "特殊类别",
          label: "特殊类别",
        },
        {
          value: "加班换休",
          label: "加班换休",
        },
      ],
      //时间段选项
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
  //当用户修改表单，重新计算天数
  watch: {
    addDialogForm: {
      handler(val) {
        const start = dayjs(val.leaveStart);
        const end = dayjs(val.leaveEnd);
        if (!isNaN(end.diff(start, "day"))) {
          let res = end.diff(start, "day");
          if (val.leaveStartPeriod == "下午") {
            res -= 0.5;
          }
          if (val.leaveEndPeriod == "上午") {
            res += 0.5;
          } else if (val.leaveEndPeriod == "下午") {
            res += 1;
          }
          val.leaveTotal = res;
        }
        const returnDay = dayjs(val.returnToWork);
        if (!isNaN(returnDay.diff(start, "day"))) {
          let ress = returnDay.diff(start, "day");

          if (val.leaveStartPeriod == "下午") {
            ress -= 0.5;
          }
          if (val.returnPeriod == "上午") {
            ress += 0.5;
          } else if (val.returnPeriod == "下午") {
            ress += 1;
          }
          val.returnTotal = ress;
        }
      },
      immediate: true,
      deep: true,
    },
    updateDialogForm: {
      handler(val) {
        const start = dayjs(val.leaveStart);
        const end = dayjs(val.leaveEnd);
        if (!isNaN(end.diff(start, "day"))) {
          let res = end.diff(start, "day");
          if (val.leaveStartPeriod == "下午") {
            res -= 0.5;
          }
          if (val.leaveEndPeriod == "上午") {
            res += 0.5;
          } else if (val.leaveEndPeriod == "下午") {
            res += 1;
          }
          val.leaveTotal = res;
        }
        const returnDay = dayjs(val.returnToWork);
        if (!isNaN(returnDay.diff(start, "day"))) {
          let ress = returnDay.diff(start, "day");

          if (val.leaveStartPeriod == "下午") {
            ress -= 0.5;
          }
          if (val.returnPeriod == "上午") {
            ress += 0.5;
          } else if (val.returnPeriod == "下午") {
            ress += 1;
          }
          val.returnTotal = ress;
        }
      },
      immediate: true,
      deep: true,
    },
  },
  created() {
    this.getNewPage();
  },
  methods: {
    handleDelete(index, row) {
      this.$confirm("此操作将永久删除该记录, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          this.$http
            .delete("users/" + row.id)
            .then()
            .catch((e) => {
              console.log(e);
            });
          this.getNewPage();

          this.$message({
            type: "success",
            message: "删除成功!",
            duration: 500,
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除",
            duration: 500,
          });
        });
    },
    addForm(form) {
      this.$http
        .post("users", form)
        .then()
        .catch((e) => {
          console.log(e);
        });
      this.getNewPage();
    },
    handleRecord(index, row) {
      this.historyDialogTableVisible = true;
      setTimeout(() => {
        this.$http
          .get("users/history/" + row.id)
          .then((res) => {
            this.historyForms = res.data;
            console.log(res);
          })
          .catch((e) => {
            console.log(e);
          });
      }, 250);
    },
    //
    createTimeFormatter(row, column) {
      var date = row[column.property];
      var day = dayjs(date);
      return day.format("YYYY-MM-DD HH:mm:ss");
    },
    handleEdit(index, row) {
      this.updateDialogForm = { ...this.leaveForms[index] };
      console.log("leaveForms", this.leaveForms, row);
      this.updateDialogFormVisible = true;
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
      this.getNewPage();
    },
    handleCurrentChange(val) {
      this.pagination.page = val;
      this.getNewPage();
    },
    getNewPage() {
      setTimeout(() => {
        this.$http
          .get("users/search/", {
            params: {
              name: this.savedSearchForm.searchname,
              page: this.pagination.page,
              size: this.pagination.size,
              leaveType: this.savedSearchForm.leaveType,
            },
          })
          .then((res) => {
            this.leaveForms = res.data.result;
            if (this.leaveForms.length == 0 && this.pagination.page > 1) {
              this.pagination.page -= 1;
              this.getNewPage();
            }
            this.pagination.count = res.data.count;
          })
          .catch((e) => {
            console.log(e);
          });
      }, 250);
    },
    //查询
    SearchEmps() {
      this.savedSearchForm.leaveType = this.searchForm.leaveType;
      this.savedSearchForm.searchname = this.searchForm.searchname;
      this.getNewPage();
    },
  },
};
</script>

<style>
#app {
  margin: 2%;
}
</style>

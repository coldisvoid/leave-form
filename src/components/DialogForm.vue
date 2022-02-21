<template>
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
        <el-input v-model="addDialogForm.reason" autocomplete="off"></el-input>
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
      <el-button @click="addDialogFormVisible = false">取 消</el-button>
      <el-button type="primary" @click="submitAddDialogForm">确 定</el-button>
    </div>
  </el-dialog>
</template>

<script>
export default {
  props: [""],
};
</script>

<style>
</style>
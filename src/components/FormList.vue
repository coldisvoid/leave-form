    <el-dialog
      title="新增请假单"
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
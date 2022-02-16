<template>
  <div id="app">
<!-- Form -->
<el-button  @click="addDialogFormVisible = true">新建</el-button>

<el-dialog title="新增请假单" :visible.sync="addDialogFormVisible">
  <el-form :model="addDialogForm">
    <el-form-item label="姓名" :label-width="formLabelWidth">
      <el-input v-model="addDialogForm.name" autocomplete="off"></el-input>
    </el-form-item>

  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="submitAddDialogForm()">确 定</el-button>
  </div>
</el-dialog>


<el-dialog title="更新请假单" :visible.sync="updateDialogFormVisible">
  <el-form :model="updateDialogForm">
    <el-form-item label="姓名" :label-width="formLabelWidth">
      <el-input v-model="updateDialogForm.name" autocomplete="off"></el-input>
    </el-form-item>

  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="updateDialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="submitUpdateDialogForm()">确 定</el-button>
  </div>
</el-dialog>

    <!-- 列表 -->
    <el-table
      :data="leaveForms"
      :row-key="row => { return row.id }"
      style="width: 100%">
      <el-table-column
        prop="id"
        label="id"
        width="180">
      </el-table-column>
      <el-table-column
        prop="name"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button
            size="mini"
            @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
          <el-button
            size="mini"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>

  </div>
</template>

<script>

export default {
  name: 'App',

  data(){
    return{
      //新增
        addDialogFormVisible: false,
        addDialogForm:{
        },
        formLabelWidth: '120px',
      //列表
      leaveForms:[],
      //修改
      updateDialogFormVisible: false,
      updateDialogForm:{
        
      },

    }
  },
  created () {
        this.$http.get('users').then(
          response => {
            this.leaveForms = response.data
          }
        ).catch(e => { console.log(e) })
  },
  methods: {
    //
    getFormList(){
        setTimeout(() =>{
        this.$http.get('users').then(
          response => {
            this.leaveForms = response.data
          }
        ).catch(e => { console.log(e) })
      },250);

      
    },
    addForm(form){
      this.$http.post('users',form).then(
        // response => {
        //   console.log(response)
        // }
      ).catch(e => { console.log(e) })
      this.getFormList()
    },

      handleEdit(index, row) {
        this.updateDialogForm={...this.leaveForms[index]}
        console.log("leaveForms",this.leaveForms,row)
        this.updateDialogFormVisible=true

      },
      handleDelete(index, row) {
        console.log("Delete:",index, row.id);
        this.$http.delete('users/'+row.id).then(
          // response => {
          //   console.log(response)
          // }
        ).catch(e => { console.log(e) })
        this.getFormList()

      },
    submitAddDialogForm(){
      this.addForm(this.addDialogForm)
      this.dialogFormVisible = false;
    },
    submitUpdateDialogForm(){
      this.addForm(this.updateDialogForm)
      this.updateDialogFormVisible = false;
    },
    },

}
</script>

<style>

</style>

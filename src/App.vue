<template>
  <div id="app">
<!-- Form -->
<el-button  @click="dialogFormVisible = true">新建</el-button>

<el-dialog title="收货地址" :visible.sync="dialogFormVisible">
  <el-form :model="dialogForm">
    <el-form-item label="姓名" :label-width="formLabelWidth">
      <el-input v-model="dialogForm.name" autocomplete="off"></el-input>
    </el-form-item>

  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="submitDialogForm()">确 定</el-button>
  </div>
</el-dialog>

    <!-- 列表 -->
    <el-table
      :data="leaveForms"
      :row-key="row => { return row.id }"
      style="width: 100%">
      <el-table-column
        prop="email"
        label="email"
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
        dialogTableVisible: false,
        dialogFormVisible: false,
        dialogForm:{
          name:"",
        },
        leaveform: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        },
        formLabelWidth: '120px',
      leaveForms:[],
      form: {
        name: '',
        desc: ''
      }

    }
  },
  created () {
        this.$http.get('users').then(
          response => {
            this.leaveForms = response.data
            console.log(this.leaveForms)
          }
        ).catch(e => { console.log(e) })
  },
  methods: {

    showForm(){
        setTimeout(() =>{
        this.$http.get('users').then(
          response => {
            this.leaveForms = response.data
            console.log(this.leaveForms)
          }
        ).catch(e => { console.log(e) })
      },250);

      
    },
    saveForm(){
      this.$http.post('users',{
        name:this.dialogForm.name,
      }).then(
        response => {
          console.log(response)
        }
      ).catch(e => { console.log(e) })
      this.showForm()
    },
      onSubmit() {
        console.log('submit!');
        this.saveForm();
      },
      handleClick(row) {
        console.log(row);
      },
      handleEdit(index, row) {
        console.log(index, row);
      },
      handleDelete(index, row) {
        console.log("Delete:",index, row.id);
        this.$http.delete('users/'+row.id).then(
          response => {
            console.log(response)
          }
        ).catch(e => { console.log(e) })
        this.showForm()

      },
    submitDialogForm(){
      this.saveForm()
      this.dialogFormVisible = false;
    },
    },

}
</script>

<style>

</style>

<template>
<div>
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
  data(){
    return{
      leaveForms:[],
      form: {
        name: '',
        desc: ''
      }
    }
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
        name:this.form.name,
        email:this.form.desc
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

      }
    },
}
</script>

<style>

</style>
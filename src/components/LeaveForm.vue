<template>
<div>
      <el-form ref="form" :model="form" label-width="80px">
      <el-form-item label="活动名称">
        <el-input v-model="form.name"></el-input>
      </el-form-item>
      <el-form-item label="email">
        <el-input type="textarea" v-model="form.desc"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">立即创建</el-button>
        <el-button>取消</el-button>
      </el-form-item>
    </el-form>
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
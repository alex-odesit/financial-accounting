<template>
   <el-card class="form-wrapper">
      <el-form ref='addItemForm' :model='formData' :rules='rules'>
         <el-form-item label='Тип' prop='type'>
            <el-select ref='selectValue' class="type-select" v-model="formData.type" placeholder="Choose type...">
               <el-option label='Прибыль' value='INCOME' />
               <el-option label='Убыток' value='OUTCOME' />
            </el-select>
         </el-form-item>
         <el-form-item label='Комментарий' prop='comment'>
            <el-input v-model="formData.comment" />
         </el-form-item>
         <el-form-item  label='Сколько' prop='value'>
            <el-input @keyup.enter.native="onSubmit" v-model.number="formData.value" />
         </el-form-item>
         <el-button @click="onSubmit" type='primary' >Добавить</el-button>
      </el-form>
   </el-card>
   
</template>




<script>
export default {
   name:'Form',
   data: () => ({
      formData:{
         type: 'INCOME',
         comment: '',
         value: 0
      },
      rules:{
         type:[{required: true, message: 'Пожалуйста, введите тип', trigger:'blur'}],
         comment:[{required: true, message: 'Пожалуйста, введите комментарий', trigger:'blur'}],
         value:[{required: true, message: 'Пожалуйста, введите комментарий', trigger:'blur'},
               {type: 'number', message: 'Данное поле заполняеться только числами!', trigger:'change'}
         ]
      }
   }),
   methods:{
      onSubmit(){
         const valueSelect = this.$refs.selectValue.value;
         this.$refs.addItemForm.validate(valid =>{
            if(valid){
               if(valueSelect === 'INCOME'){
                  this.$emit('submitForm',this.formData);
                  if(this.formData.value==0){
                     this.$emit('valueSelect','');
                  }else{
                     this.$emit('valueSelect',valueSelect);
                  }
                  this.$refs.addItemForm.resetFields();
               }
               else{
                  this.formData.value = -this.formData.value;
                  this.$emit('submitForm',this.formData);
                  if(this.formData.value==0){
                     this.$emit('valueSelect','');
                  }else{
                     this.$emit('valueSelect',valueSelect);
                  }
                  this.$refs.addItemForm.resetFields();
               }
            }
         })
      }
   }
}
</script>




<style scoped>
.form-wrapper{
    max-width: 500px;
    margin: 0 auto;
}
.type-select{
   width: 100%;
}
</style>
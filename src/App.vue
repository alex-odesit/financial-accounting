<template>
  <div id="app">
    <Form @submitForm='onFormSubmit' @valueSelect='valueSelect' />
    <TotalBalance :select='select' :total="totalBalance" />
    <BadgetList :list='list' @deleteItem='onDeleteItem' />
  </div>
</template>



<script>
import BadgetList from './components/BadgetList.vue';
import TotalBalance from './components/TotalBalance.vue';
import Form from './components/Form.vue';


export default {
  name: 'App',
  components: {
    BadgetList,
    TotalBalance,
    Form
  },
  data: () => ({
    select:'',
    list:{
      1:{
        type: 'INCOME',
        value: 100,
        comment: 'Какой-то коментарий',
        id: 1
      },
      2:{
        type: 'OUTCOME',
        value: -50,
        comment: 'Ещё какой-то комментарий',
        id: 2
      },
    }
  }),
  computed:{
    totalBalance(){
      return Object.values(this.list).reduce((acc, item) => acc + item.value,0);
    },
  },
  methods:{
    onDeleteItem(id){
      this.$delete(this.list,id);
    },
    onFormSubmit(data){
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj);
    },
    valueSelect(select){
      this.select = select;
      return this.select;
    }
  },

}
</script>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}
</style>

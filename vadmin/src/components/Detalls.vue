<template>
  <div class="details container">
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h1 class="page-header">
      {{customer.name}}
      <span class="pull-right">
    <router-link v-bind:to="'/edit/'+customer.id" class="btn btn-primary">编辑</router-link>
      <button class="btn btn-danger" @click="deleteCustomer(customer.id)">删除</button>
      </span>

    </h1>
    <ul>
      <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">
        {{customer.phone}}
        </span></li>
             <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">
        {{customer.email}}
        </span></li>

    </ul>
     <ul>
      <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">
        {{customer.education}}
        </span></li>
             <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">
        {{customer.graduationschool}}
        </span></li>

    </ul>
      <ul>
      <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">
        {{customer.profession}}
        </span></li>
             <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">
        {{customer.profile}}
        </span></li>

    </ul>
  </div>
</template>

<script>
export default {
  name: 'details',
  data () {
    return {
      customer:""
    }
  },
   methods:{
    fetch(id){
      this.$http.get('http://localhost:3000/users/'+id)
      .then((responce) => {
        this.customer=responce.body;
      }).catch((err) => {

      });
    },
    deleteCustomer(id){
     this.$http.delete('http://localhost:3000/users/'+id)
     .then((response)=>{
       this.$router.push({path:'/',query:{alert:'用户删除成功'}});
     })
    }
  }
  ,
  created(){
    this.fetch(this.$route.params.id);
  }
}
</script>
</style>

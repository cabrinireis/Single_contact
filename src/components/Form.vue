<template>

<div class="container" >
  
  <div class="formul">
  <form @submit.prevent="enviar">
      <div class="form-row">
        <div class="form-group col-md-6">
          <label :class="{ invalid: $v.nome.$dirty && $v.nome.$invalid}"  for="inputName" class="label">Nome</label>
          <input :class="{ invalid: $v.nome.$dirty && $v.nome.$invalid}" type="text" class="form-control" id="inputName" v-model="nome">
        </div>
      </div>
      <div class="form-row">
        <div class="form-group col-md-6" >
          <label :class="{ invalid: $v.sobrenome.$invalid && $v.sobrenome.$dirty}" for="inputSobrenome" class="label">Sobre Nome</label>
          <input :class="{ invalid: $v.sobrenome.$invalid && $v.sobrenome.$dirty}" type="text" class="form-control" id="inputSobrenome" v-model="sobrenome">
        </div>
      </div>
      <div class="form-row">
        <div class="form-group col-md-6">
          <label :class="{ invalid: $v.cpf.$invalid && $v.cpf.$dirty}" for="inputcpf">CPF</label>
          <input :class="{ invalid: $v.cpf.$invalid && $v.cpf.$dirty}" type="" class="form-control" id="inputcpf" v-model="cpf" maxlength="11" >
        </div>
      </div>
      <div class="form-row">
        <div class="form-group col-md-6">
          <label :class="{ invalid: $v.telefone.$invalid && $v.telefone.$dirty}" for="inputPhone">Telefone</label>
          <input :class="{ invalid: $v.telefone.$invalid && $v.telefone.$dirty}" type="text" class="form-control"  id="inputPhone" v-model="telefone" >
        </div>
      </div>
      <div class="form-row">
        <div class="form-group col-md-6">
          <label :class="{ invalid: $v.email.$invalid && $v.email.$dirty }" for="inputEmail">E-mail</label>
          <input :class="{ invalid: $v.email.$invalid && $v.email.$dirty }" type="email" class="form-control" id="inputEmail" v-model="email">
          
        </div>
      </div>
      
  
      <div>
        <button type="submit"  class="btn btn-primary"  >ENVIAR</button>
      </div>
    </form>
  </div>
</div>
</template>


<script>
//import { bus } from '../main'
import { required, email, numeric } from 'vuelidate/lib/validators'

export default {
    mounted(){
      this.$bus
      
    },
    name: 'Formulario',
    data() {
      return{
        nome: '',
        sobrenome: '',
        telefone: '',
        cpf: '',
        email: ''
      }
    },
    methods: {
      enviar () {
        var resource = this.$resource('http://localhost:3000/clientes');

        if (!this.$v.$invalid) {
          resource.save({

            nome: this.nome,
            sobrenome: this.sobrenome,
            telefone: this.telefone,
            cpf: this.cpf,
            email: this.email

          }).then(response => {
            console.log(response)
          }, response => {
            console.log(response)
          });
          this.resetar()
        } else {
          this.$v.$touch()
        }
      },
      resetar () {
        this.nome= '',
        this.sobrenome= '',
        this.cpf= '',
        this.telefone= '',
        this.email= '',
        this.$v.$reset()
      }
    },
    
    validations: {
        
        nome: {
          required,
        },
        sobrenome: {
          required,
        },
        cpf: {
          required,
          numeric
        },
        telefone: {
         required,
         numeric
        },
        email: {
          required,
          email
        } 
    },
}
</script>
<style>

.form-control{
  width: 300px;

}
form{
  padding: 20px 40px;
}
.formul{
  display: inline-block;
  background-color: rgba(190, 185, 185, 0.425);
  border-radius: 10px;
}
.form-group{
  text-align: left;
}
.form-control.invalid {
  border: red 1px solid;
}

</style>

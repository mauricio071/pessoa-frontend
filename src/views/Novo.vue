<template>
    <div class="home">
        <h1 class="text-center mt-4 mb-4">Novo</h1>
        <div class="col-8 m-auto">
            <form>
                <input class="form-control" type="text" name="nome" v-model="form.nome" placeholder="Nome:"><br>
                <input class="form-control" type="text" name="data" v-model="form.data" placeholder="Data:"><br>
                <input class="form-control" type="text" name="peso" v-model="form.peso" placeholder="Peso:"><br>
                <input class="form-control" type="text" name="sexo" v-model="form.sexo" placeholder="Sexo:"><br>
                <input class="form-control" type="text" name="cpf" v-model="form.cpf" placeholder="CPF:"><br>
                <input class="btn btn-primary" value="Cadastrar" @click.prevent="store">
            </form>
        </div>
    </div>
</template>

<script>
import {apiPublic} from '../api/service'

export default {
    name: 'Home',

    data(){
        return {
            form: {
                nome: null,
                data: null,
                peso: null,
                sexo: null,
                cpf: null,
            }
        }
    },
  
    methods: {
        store() {
            apiPublic.post(`novo/pessoa`, this.form)
            .then((response) => {
                console.log(response)
                //window.location.href = "http://192.168.15.11:8080/"
            })
            .catch(e => {
                this.errors.push(e)
            })
        },
    }
} 
</script>



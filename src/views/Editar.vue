<template>
    <div class="home">
        <h1 class="text-center mt-4 mb-4">Editar</h1>
        <div class="col-8 m-auto">
            <form>
                <input class="form-control" type="text" name="nome" v-model="form.nome"><br>
                <input class="form-control" type="text" name="data" v-model="form.data"><br>
                <input class="form-control" type="text" name="peso" v-model="form.peso"><br>
                <input class="form-control" type="text" name="sexo" v-model="form.sexo"><br>
                <input class="form-control" type="text" name="cpf" v-model="form.cpf"><br>
                <input class="btn btn-primary" value="Editar" @click.prevent="editar(form.id)">
            </form>
        </div>
    </div>
</template>

<script>
import {apiPublic} from '../api/service'

export default {
    name: 'Home',
    props: ['pessoa'],

    data(){
        return {
            form: {
                nome: 'null',
                data: null,
                peso: null,
                sexo: null,
                cpf: null,
            }
        }
    },
    
    created() {
        this.form.id = this.pessoa.id
        this.form.nome = this.pessoa.nome
        this.form.data = this.pessoa.data
        this.form.peso = this.pessoa.peso
        this.form.sexo = this.pessoa.sexo
        this.form.cpf = this.pessoa.cpf
    },

    methods: {
        editar(id) {
            apiPublic.post(`editar/${id}`, this.form)
            .then(() => {
                window.location.href = "http://192.168.15.11:8080/"
            })
            .catch(e => {
                this.errors.push(e)
            })
        },
    }
} 
</script>



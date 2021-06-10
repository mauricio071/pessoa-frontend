<template>
    <div class="container">
        
        <div v-if="novo === true">
            <Novo/>
        </div>

        <div v-if="editar === true">
            <Editar :pessoa='pessoa'/> 
        </div>

        <div v-if="novo === false && editar === false">
            <div class="text-center mt-4 mb-4">
                <button class="btn btn-success" @click.prevent="criar">novo</button>
            </div>
            <table class="table">
                <thead>
                    <tr>
                    <th scope="col">#</th>
                    <th scope="col">Nome</th>
                    <th scope="col">Data</th>
                    <th scope="col">Peso</th>
                    <th scope="col">Sexo</th>
                    <th scope="col">CPF</th>
                    <th scope="col">Funções</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(pessoa, index) in dados" :key='index'>
                        <th scope="row">{{pessoa.id}}</th>
                        <td>{{pessoa.nome}}</td>
                        <td>{{pessoa.data}}</td>
                        <td>{{pessoa.peso}}</td>
                        <td>{{pessoa.sexo}}</td>
                        <td>{{pessoa.cpf}}</td>
                        <td>
                            <a class="btn btn-primary" @click.prevent="alterar(pessoa.id)">Editar</a>
                            <a class="btn btn-danger" @click.prevent="excluir(pessoa.id)">Excluir</a>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div> 
    </div>
</template>

<script>
import {apiPublic} from '../api/service'
import Novo from './Novo.vue'
import Editar from './Editar.vue'

export default {
    name: 'Home',

    components: {
        Novo,
        Editar,
    },

    data() {
        return {
            dados: null,
            novo: false,
            editar: false,
            pessoa: null,
        }
    },

    created(){
        this.getPessoas()
    },

    methods: {
        getPessoas() {
            apiPublic.get(`pessoas`)
            .then(response => {
                this.dados = response.data
            })
            .catch(e => {
                this.errors.push(e)
            })
        },

        criar() {
            this.novo = !this.novo
        },

        alterar(id) {
            apiPublic.get(`editar/${id}`)
            .then(response => {
                this.pessoa = response.data
                this.editar = !this.editar
            })
            .catch(e => {
                this.errors.push(e)
            })
        },

        excluir(id) {
            apiPublic.get(`excluir/${id}`)
            .then(() => {
                this.getPessoas()
            })
            .catch(e => {
                this.errors.push(e)
            })
        },
    }
}
</script>

<script lang="ts">
import type IReceita from '@/interfaces/IReceita';
import BotaoPrincipal from './BotaoPrincipal.vue';
import CardReceita from './CardReceita.vue';
import { obterReceitas } from '@/http/receitashttp'
import type { PropType } from 'vue';
import {itemDeLista1EstaEmLista2} from '../operacoes/listas';

export default {
    props:{
        ingredientes: {type:Array as PropType<string[]>, required:true}
    },
    data(){
        return {
            receitas: [] as IReceita[]
        }
    },
    components: { BotaoPrincipal, CardReceita },
    emits: ['SelecionarIngredientes'],
    async created(){
        const receitas = await obterReceitas()
        this.receitas = receitas.filter((receita)=>{
            return itemDeLista1EstaEmLista2(receita.ingredientes,this.ingredientes)
        })
    }
}
</script>

<template>
    <article class="mostrar-receitas">
        <h1 class="titulo-receitas cabecalho">Receitas</h1>
        <h2 class="paragrafo subtitulo-receitas">Resultados encontrados: {{ receitas.length }}</h2>
        <section v-if="receitas.length " class="section-mostrar-receitas">
            <p class="paragrafo">Veja os resultados de receitas que encontramos com os ingredientes que você tem por aí!</p>
            <ul class="lista-receitas">
                <li v-for="receita in receitas">
                    <CardReceita :receita="receita"/>
                </li>
            </ul>
        </section>
        <section v-else class="section-mostrar-receitas">
            <p class="paragrafo">Ops, não encontramos resultados para suas combinações, vamos tentar de novo?</p>
            <img  src="../assets/imagens/sem-receitas.png" alt="" class="not-found">
        </section>
        <BotaoPrincipal
            v-on:click="$emit('SelecionarIngredientes')"
            texto="Selecionar ingredientes!"
        />
    </article>
</template>

<style scoped>
.lista-receitas{
    margin-bottom: 1rem;
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}
.section-mostrar-receitas{
    display: flex;
    flex-direction: column;
    align-items: center;
    gap:1rem;
}
.titulo-receitas{
    color: var(--verde-medio, #3D6D4A);
    display: block;
    margin-bottom: 1.5rem;
}
.subtitulo-receitas{
    color:#3D6D4A
}
.mostrar-receitas{
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>
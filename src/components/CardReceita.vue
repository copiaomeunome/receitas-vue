<script lang="ts">
import type IReceita from "@/interfaces/IReceita"
import type {PropType} from 'vue'
export default {
    props:{
        receita:{type:Object as PropType<IReceita>, required:true}
    }
}
</script>

<template>
    <article class="card-receita">
        <img :src="`/imagens/receitas/${receita.imagem}`" alt="" class="imagem-card">
        <p class="paragrafo">{{ receita.nome }}</p>
    </article>
</template>

<style scoped>
.card-receita{
    width: 19.5rem;
    border-radius: 1rem;
    background: var(--branco, #FFF);
    box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
    height: 100%;
    overflow:hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
}
.imagem-card{
    width: 100%;
}

</style>
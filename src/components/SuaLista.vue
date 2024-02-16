<script lang="ts">
import Tag from './Tag.vue'
import type { PropType } from 'vue';
export default {
    props: {
        ingredientes: {type:Array as PropType<string[]>, required:true}
    },
    components: { Tag }
}
</script>

<template>
    <section>
        <span class="subtitulo lg sua-lista-texto">Sua lista:</span>
        <ul v-if="ingredientes.length" class="ingredientes-sua-lista">
            <li v-for="ingrediente in ingredientes" v-bind:key="ingrediente">
                <Tag 
                :texto="ingrediente" :ativa="true"
                />
            </li>
        </ul>
        <p v-else class="paragrafo lista-vazia">
            <img src="../assets/imagens/icones/lista-vazia.svg" alt="">
            Sua lista está vazia, selecione um ingrediente para iniciar.
        </p>
    </section>
</template>

<style scoped>

.sua-lista-texto {
  color: var(--coral, #F0633C);
  display: block;
  text-align: center;
  margin-bottom: 1.5rem;
}

.ingredientes-sua-lista {
  display: flex;
  justify-content: center;
  gap: 1rem 1.5rem;
  flex-wrap: wrap;
}



.lista-vazia {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.25rem;

  color: var(--coral, #F0633C);
  text-align: center;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>
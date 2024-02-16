<script lang="ts">
import SelecionarIngredientes from './SelecionarIngredientes.vue';
import SuaLista from './SuaLista.vue';
import MostrarReceitas from './MostrarReceitas.vue';

type Pagina = 'MostrarReceitas' | 'SelecionarIngredientes'

export default {
    data() {
        return {
            ingredientes: [] as string[],
            conteudo: 'SelecionarIngredientes' as Pagina
        };
    },
    components: { SelecionarIngredientes, SuaLista, MostrarReceitas },
    methods: {
        adicionarIngrediente(ingrediente:string){
            this.ingredientes.push(ingrediente)
        },
        removerIngrediente(ingrediente:string){
            this.ingredientes.splice(this.ingredientes.indexOf(ingrediente), 1);
        },
        navegar(pagina:Pagina){
            this.conteudo=pagina
        }
    }
}
</script>

<template>
    <main class="conteudo-principal">
        <SuaLista :ingredientes="ingredientes"/>
        <KeepAlive include="SelecionarIngredientes">
            <SelecionarIngredientes v-if="conteudo==='SelecionarIngredientes'"
                @remover-ingrediente="removerIngrediente($event)"
                @adicionar-ingrediente="adicionarIngrediente($event)"
                @buscar-receitas="navegar('MostrarReceitas')"
            />
            <MostrarReceitas
                @selecionar-ingredientes="navegar('SelecionarIngredientes')"
                v-else-if="conteudo === 'MostrarReceitas'"
                :ingredientes="ingredientes"
            />
        </KeepAlive>
    </main>
</template>

<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #FFFAF3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

</style>
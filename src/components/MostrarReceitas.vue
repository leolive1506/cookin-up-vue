<script lang="ts">
import type { IReceita } from "@/interfaces/IReceita"
import { getReceitas } from '@/http';
import CardReceita from './CardReceita.vue'
import BotaoPrincipal from './BotaoPrincipal.vue'
import type { PropType } from "vue";

export default {
  components: { CardReceita, BotaoPrincipal },
  props: {
    ingredientes: { type: Array as PropType<string[]>, required: true }
  },
  data() {
    return {
      receitas: [] as IReceita[]
    }
  },
  async created() {
    const responseReceitas = await getReceitas()
    this.receitas = responseReceitas.filter((receita: IReceita) => {
      return receita.ingredientes.every((ingrediente: string) => this.ingredientes.includes(ingrediente))
    })
  },
  emits: ['editarReceitas']
}
</script>
<template>
  <section class="mostrar-receitas">
    <h1 class="cabecalho titulo-receitas">Receitas</h1>

    <p class="paragrafo-lg resultados-encontrados">
      Resultados encontrados: 
      {{ receitas.length }}
    </p>

    <div v-if="receitas.length" class="receitas-wrapper">
      <p class="paragrafo-lg informacoes">
        Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!
      </p>

      <ul class="receitas">
        <li v-for="receita in receitas" :key="receita.nome">
          <card-receita :receita="receita"/>
        </li>
      </ul>
    </div>

    <div v-else class="receitas-nao-encontradas">
      <p class="paragrafo-lg receitas-nao-encontradas__info">
        Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?
      </p>

      <img src="../assets/imagens/sem-receitas.png"
        alt="Desenho de um ovo quebrado. A gema tem um rosto com uma expressão triste.">
    </div>

    <botao-principal texto="Editar lista" @click="$emit('editarReceitas')" />
  </section>
</template>

<style scoped>
.mostrar-receitas {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.titulo-receitas {
  color: var(--verde-medio, #3D6D4A);
  margin-bottom: 1.5rem;
}

.resultados-encontrados {
  color: var(--verde-medio, #3D6D4A);
  margin-bottom: 0.5rem;
}

.receitas-wrapper {
  margin-bottom: 3.5rem;
}

.informacoes {
  margin-bottom: 2rem;
}

.receitas {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.receitas-nao-encontradas {
  margin-bottom: 2rem;
}

.receitas-nao-encontradas__info {
  margin-bottom: 0.5rem;
}

@media only screen and (max-width: 767px) {
  .receitas-wrapper {
    margin-bottom: 2rem;
  }
}
</style>
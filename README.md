# Events emit
```ts
export default {
  data() {
    return {
      selecionado: false
    }
  },
  methods: {
    aoClicar() {
      this.selecionado = !this.selecionado

      if (this.selecionado) {
        this.$emit('adicionar', this.ingrediente)
      }
    }
  },
  emits: ['adicionar']
}
```

# KeepAlive
- manter estado do componente "vivo"
- guarda estado em cache
- possivel especificar qual componentes quer deixar em cache, passando o nome do componente
```vue
<template>
<keep-alive include="selecionar-ingredientes">
  <selecionar-ingredientes
    v-if="conteudo === 'SelecionarIngredientes'"
    @adicionar-ingrediente="adicionarIngrediente"
    @remover-ingrediente="removerIngrediente"
    @buscar-receitas="navegar('MostrarReceitas')"
  />
  <mostrar-receitas
    v-else
    @editar-receitas="navegar('SelecionarIngredientes')"
  />
</keep-alive>
</template>
<script lang="ts">
// no componente selecionar-ingredientes
export default {
  name: 'selecionar-ingredientes',
}
</script>
```
# Single file componentes
- componente de arquivo único (Html, css e js mesmo arquivo)

# style scoped
- vue adicionar atribues com ids únicos aos componentes / tags
- não afetando estilização dos filhos
- utiliza por baixo dos panos, PostCSS
- para deixar visivel aos filhos para tirar atributo scoped
  - posso ter um style scoped e um global normalmente
- [clique para ver feature css no vue](https://vuejs.org/api/sfc-css-features.html)
# Geral
## Comandos
- gerar estrutura de pastas no terminal
```sh
tree
# windows
tree /f
```


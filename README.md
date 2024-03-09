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
<template>
  <div id="app">
    <h1>Jogo da Forca</h1>

    <section v-if="tela === 'inicio'" id="inicio">
      <Formulario
        v-if="etapa === 'palavra'"
        title="Defina a palavra"
        button="Próximo"
        :action="setPalavra"
      />
      <Formulario
        v-if="etapa === 'dica'"
        title="Defina a dica"
        button="Iniciar jogo =)"
        :action="setDica"
      />
    </section>

    <section v-if="tela === 'jogo'" id="jogo">
      <Jogo
        :erros="erros"
        :palavra="palavra"
        :dica="dica"
        :verificarLetra="verificarLetra"
        :etapa="etapa"
        :letras="letras"
        :jogar="jogar"
        :jogarNovamente="jogarNovamente"
      />
    </section>
  </div>
</template>

<script>
import './css/global.css'
import Formulario from './components/Formulario.vue'
import Jogo from './components/Jogo.vue'

export default {
  name: 'App',
  data() {
    return {
      tela: 'inicio',
      etapa: 'palavra',
      palavra: '', // palavra que será salva para o jogo
      dica: '',
      erros: 0,
      letras: []
    }
  },

  components: {
    Formulario,
    Jogo
  },

  methods: {
    setPalavra(palavra) {
      this.palavra = palavra
      this.etapa = 'dica' // Aqui eu to trocando o valor da etapa, para que possa trocar o formulário também
    },

    // Nessa função, após eu digitar a dica, ele irá para a próxima etapa, que é o inicio do jogo
    setDica(dica) {
      this.dica = dica
      this.tela = 'jogo'
      this.etapa = 'jogo'
    },

    verificarLetra(letra) {
      return this.letras.find(item => item.toLowerCase() === letra.toLowerCase())
    },

    jogar(letra){
      //adiciona letra jogada
      this.letras.push(letra)

      //Validar erro
      this.verificarErros(letra)
    },

    verificarErros(letra) {
      // o indexOf procura dentro da nossa string a posição da letra
      if(this.palavra.toLowerCase().indexOf(letra.toLowerCase()) >= 0) {
        return this.verificarAcertos()
      }

      // Count dos erros
      this.erros++

      if(this.erros === 6) {
        this.etapa = 'enforcado'
      }
    },

    verificarAcertos() {
      //Aqui eu acesso a palavra e crio um array com todas as letras separadas
      // new Set é uma classe que cria estruturas com valores únicos
      let letrasUnicas = [...new Set(this.palavra.split(''))]
      if(letrasUnicas.length === (this.letras.length - this.erros)){
        this.etapa = 'ganhador'
      }
    },

     jogarNovamente() {
    this.palavra = ''
    this.dica = ''
    this.erros = ''
    this.letras = []
    this.tela = 'inicio'
    this.etapa = 'palavra'
  }
  }
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>



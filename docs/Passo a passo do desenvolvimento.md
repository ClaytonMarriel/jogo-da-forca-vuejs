# jogo-da-forca

-> Escondendo componentes do HTML
-> Formulário será um componente que será reutilizado em algumas partes da aplicação
-> Propriedades dos componentes
-> v-model: Toda vez que digitar o valor no input, o valor da variável é atualizado
-> Para ocultar uma parte do html, eu criei uma variável dentro do data e fiz o v-if para verificar se a tal palavra
estava no elemento
-> Eventos do botão:
* No Formulario.vue, criei uma action, que recebia uma Function (setPalavra, setDicas)
* Esse formulário passou como propriedade como uma função
* Sendo chamada ao definir a palavra do jogo
* Sendo chamada ao definir a dica que será dada
* Componente para criar o jogo
* Componente Forca
* Passar propriedades por mais de um componente
* Adicionei uma prop em App.vue = erros, que receberá zero
* Adicionado uma prop em Jogo, onde erros receberá um Number
* Adicionado uma prop em Forca, onde erros receberá também um Number
* Adicionando template strings, e fazendo o bind no src, foi possível deixar as imagens dinâmicas
* Componente Palavra
* Passamos a palavra enviada pelo input e a dica como propriedade para o componente Jogo e Palavra
* Criamos uma div com v-for para percorrer a palavra, letra a letra
* Criei uma função para verificar a letra, se está correta ou não. Se estiver correta, será exibida.
* Componente Teclado
* Irá receber a propriedade letras
* No componente do teclado, foi criado um button que percorre todo o alfabeto usando v-for para exibir esse teclado 
no jogo
* No App.vue, foi criado a função "jogar", onde ao clicar em qualquer letra do teclado ele começa a jogar
* Função jogar foi passada como propriedade no componente Jogo e no componente Teclado
* Função para validar erros, que é chamada/executada dentro da função jogar
* Função verificar erros, faz a busca pelas letras incorretas e incrementa na variável erros
* Função verificar acertos, crio uma variável que vai receber um array de valores únicos, utilizando o Set e o split pra dividir a palavra em letras separadas e verifica se a quantidade de letras digitadas pelo usuário subtraindo pela quantidade de erros for igual o tamanho da variável criada acima, é sinal de que o usuário ganhou
* Componente Final -  Onde irá informar o resultado para o usuário através de uma mensagem
* Botão Jogar novamente criado
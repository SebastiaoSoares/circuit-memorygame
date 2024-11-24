# Projeto Jogo da Memória - Circuitos Digitais

## Índice
- [Sobre o projeto](#sobre-o-projeto);
- [Equipe](#equipe);
- [Simulador](#simulador);
- [Uso](#uso);
- [O circuito](#o-circuito);

## Sobre o projeto
Projeto desenvolvido da disciplina de Circuitos Digitais, do primeiro semestre do bacharelado em Ciência da Computação na Universidade Federal do Cariri (UFCA), com o objetivo de trabalhar os conceitos aprendidos em sala, a respeito de estruturas de memória (circuitos sequenciais).
A proposta consiste em um jogo da memória, onde a visualização das "peças" é feita com Displays Hexadecimais e os valores escondidos poder ser números de 0 a F (hex). A jogabilidade é feita por meio de botões que acionam contadores e registradores de modo a construir a escolha de peças, a alternância de jogadores, registro das pontuações e definição de um vencedor.

## Equipe
- [Bruno Macedo (GitHub)](https://github.com/brunom-dev);
- [Sebastião Soares (GitHub)](https://github.com/sebastiaosoares);
- **Professor:** [Ramon Nepomuceno (e-mail institucional)](mailto:ramon.nepomuceno@ufca.edu.br).

## Simulador
O simulador utilizado foi o software de prototipagem, Logisim ([download](https://sourceforge.net/projects/circuit/) - externo).

## Uso
A jogabilidade funciona da forma descrita abaixo.
1. Depois de iniciada a simulação, podem ser utilizados os botões "LINHA" e "COLUNA" para alternar entre as peças.
2. Ao escolher, utiliza-se "CONFIRMA":
   - a primeira vez para escolher uma peça;
   - a segunda, para escolher a próxima peça;
   - e a terceira, para contabilizar a pontuação e mudar de jogador.
3. Após todas as peças serem descobertas, LEDs exibem o vencedor ou indicam empate.

## O circuito
Nesta seção, será detalhada a lógica por trás do Jogo da Memória e o funcionamento do circuito.

<div align="center">
   <br><img width="50%" src="docs/0.png"><br>
   <i>Imagem da parte principal do circuito.</i><br>
</div>

### 1. Registro e captação das coordenadas
<div align="center">
   <br><img width="50%" src="docs/1.png"><br>
</div>

### 2. 
<div align="center">
   <br><img width="50%" src="docs/2.png"><br>
</div>

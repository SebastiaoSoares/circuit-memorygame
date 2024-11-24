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
   <br><img width="30%" src="docs/1.png"><br>
</div> <br>
Essa parte do circuito é responsável pela captação e registro das coordenadas selecionadas pelos jogadores no tabuleiro, armazenando-as em linha (LIN) e coluna (COL).

   - <strong>Botões de entrada (LINHA e COLUNA)</strong> <br>
        Esses botões atuam como sinais de controle para os flip-flops tipo D, responsáveis por registrar as coordenadas. Quando pressionados, alteram os valores das saídas correspondentes à linha (LIN) ou à coluna (COL).

   - <strong>Flip-Flops tipo D</strong> <br>
        Cada flip-flop registra e armazena o valor correspondente à linha ou coluna. O valor atualizado é exibido na saída ("LIN" e "COL"), representando as coordenadas escolhidas.

   - <strong>Saídas "x" e "y"</strong> <br>
        As saídas combinadas das coordenadas (x para coluna, y para linha) são utilizadas pelo circuito principal para acessar as posições do tabuleiro.



### 2. Gerenciador de Estados
<div align="center">
   <br><img width="30%" src="docs/2.png"><br>
</div> <br>
O gerenciador de estados é responsável por controlar o fluxo de estados do jogo, alternando entre os diferentes estágios da jogabilidade. Ele utiliza um flip-flop tipo D e portas lógicas para definir qual estado o jogo deve estar em um determinado momento.

   - <strong>Flip-Flop tipo D</strong> <br>
         O flip-flop armazena o estado atual do jogo. Quando o botão "CONFIRMA" é pressionado, ele gera um pulso de clock, permitindo que o valor presente na entrada "D" seja capturado e armazenado na saída "Q". Isso define o estado atual do jogo.
   
   - <strong> Portas AND </strong> <br>
         As portas AND recebem sinais dos estados anteriores e o sinal do botão CONFIRMA para calcular a transição entre os estados state0, state1, state2, e state3.

   - <strong> Estados (state0, state1, state2, state3) </strong> <br>
         Cada estado corresponde a uma fase específica do jogo:

        - <strong>state0</strong>: Seleção da primeira peça.
        - <strong>state1</strong>: Seleção da segunda peça.
        - <strong>state2</strong>: Confirmação das peças selecionadas.
        - <strong>state3</strong>: Alternância de jogador e atualização da pontuação. Após atingir o state3, a máquina de estados é resetada, retornando ao estado inicial (state0) para reiniciar o processo com o próximo jogador.





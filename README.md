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

   - <strong>Flip-Flops tipo D</strong> <br />
        Cada flip-flop registra e armazena o valor correspondente à linha ou coluna. O valor atualizado é exibido na saída ("LIN" e "COL"), representando as coordenadas escolhidas.

   - <strong>Saídas "x" e "y"</strong> <br />
        As saídas combinadas das coordenadas (x para coluna, y para linha) são utilizadas pelo circuito principal para acessar as posições do tabuleiro.
<br>

### 2. Gerenciador de Estados
<div align="center">
   <br><img width="30%" src="docs/2.png"><br>
</div> <br>
O gerenciador de estados é responsável por controlar o fluxo de estados do jogo, alternando entre os diferentes estágios da jogabilidade. Ele utiliza um flip-flop tipo D e portas lógicas para definir qual estado o jogo deve estar em um determinado momento.

   - <strong>Flip-Flop tipo D</strong> <br>
         O flip-flop armazena o estado atual do jogo. Quando o botão "CONFIRMA" é pressionado, ele gera um pulso de clock, permitindo que haja o avanço do estado atual para o próximo.
   - <strong> Portas AND </strong> <br>
         As portas AND recebem sinais dos estados anteriores e o sinal do botão CONFIRMA para calcular a transição entre os estados state0, state1, state2, e state3.

   - <strong> Estados (state0, state1, state2, state3) </strong> <br>
         Cada estado corresponde a uma fase específica do jogo:

        - <strong>state0</strong>: Seleção da primeira peça.
        - <strong>state1</strong>: Seleção da segunda peça.
        - <strong>state2</strong>: Confirmação das peças selecionadas.
        - <strong>state3</strong>: Alternância de jogador e atualização da pontuação. Após atingir o state3, a máquina de estados é resetada, retornando ao estado inicial (state0) para reiniciar o processo com o próximo jogador.
<br>

### 3. Gerenciador dos LED´S
<div align="center">
   <br><img width="30%" src="docs/3.png"><br>
</div> <br>

O demultiplexador (DMX) é responsável por controlar qual LED será aceso, indicando a peça atual que o jogador está percorrendo no tabuleiro. Ele utiliza as coordenadas registradas (XY) para selecionar a saída correspondente.

   - <strong>Entrada do DMX</strong>
      - O valor constante 1 é aplicado à entrada do demultiplexador. Isso significa que ele sempre terá um sinal ativo para ser enviado.
      - A variável de controle são as coordenadas XY (linha e coluna) provenientes do registro de coordenadas. Elas determinam qual saída será ativada.
      
   - <strong>Saídas do DMX</strong>
      - As saídas do demultiplexador correspondem aos túneis correspondente a cada LED do tabuleiro, com cada saída ativando o LED da peça atual que o jogador está percorrendo.
    
Na prática temos que ao navegar pelo tabuleiro utilizando os botões de controle (LINHA e COLUNA), o DMX atualiza a saída correspondente com base no valor das coordenadas registradas, acendendo o LED que indica a posição atual.

<br>


### 4. Registrador das posições selecionadas
<div align="center">
   <br><img width="30%" src="docs/4.png"><br>
</div> <br>

Este circuito é responsável por armazenar as coordenadas das posições escolhidas no tabuleiro durante as etapas de seleção das peças. Ele utiliza flip-flops tipo D e portas lógicas para gerenciar e registrar as posições para cada jogada.

   - <strong> Entrada de Controle </strong> <br>
       O botão "CONFIRMA" serve como sinal de controle. Ele é usado para permitir o registro das coordenadas selecionadas, gerando um pulso que ativa o armazenamento nos flip-flops correspondentes.

   - <strong> Estados State0 e State1 </strong> <br>
        O controle do circuito é dividido em dois estados principais:
       - State0: Registra as coordenadas da primeira peça selecionada (LIN1 e COL1).
       - State1: Registra as coordenadas da segunda peça selecionada (LIN2 e COL2).
       
   - <strong> Flip-Flops Tipo D </strong> <br> 
     Cada flip-flop armazena um valor de coordenada:
     - LIN1 e COL1 armazenam as coordenadas da primeira peça.
     - LIN2 e COL2 armazenam as coordenadas da segunda peça.

   - <strong> Portas AND </strong> <br> 
      As portas AND garantem que o registro só ocorra quando o botão "CONFIRMA" é pressionado e o circuito está no estado correto (state0 ou state1).

   - <strong> Saídas </strong> <br>
     As combinações das saídas dos flip-flops (savedXY1 e savedXY2) representam as coordenadas armazenadas de cada peça selecionada.


<br>


### 5. Multiplexadores para Seleção de Peças
<div align="center">
   <br><img width="30%" src="docs/5.png"><br>
</div> <br>

Esses multiplexadores (MUX) são responsaveis por manter a primeira peça selecionada ativa no tabuleiro enquanto o jogador escolhe a segunda peça do par.

- <strong>Entradas</strong>
     - Os multiplexadores recebem entradas que representam as posições possíveis no tabuleiro. Cada posição é associada a uma coordenada (linha e coluna) do tabuleiro.
     - As coordenadas salvas (savedXY1 e savedXY2) são usadas como sinais de controle.
- <strong>MUX 1:</strong> Mantém ativa a posição correspondente à primeira peça selecionada, utilizando as coordenadas salvas em savedXY1
- <strong>MUX 2:</strong> Ativa a posição correspondente à segunda peça selecionada, utilizando as coordenadas salvas em savedXY2
- <strong>Saidas</strong>
     - <strong>valueXY1</strong> Mantém a ativação da primeira peça, garantindo que ela continue iluminada durante a escolha da segunda peça.
     - <strong>valueXY2:</strong> Ativa a segunda peça com base na nova seleção do jogador.
<br>
Esse é um funcionamento essencial no jogo da memória, pois assim possibilita os jogadores memorizarem as peças e suas respectivas posições durante o andamento do jogo.

<br>


### 6. Estrutura de Verificação de Acerto
<div align="center">
   <br><img width="30%" src="docs/6.png"><br>
</div> <br>

Estrutura responsável por comparar os valores das peças selecionadas e determinar se houve um acerto, gerando um sinal para indicar o resultado. Ele utiliza comparadores e portas lógica combinacionais para realizar a verificação.

- <strong>Entradas</strong>
   - valueXY1 e valueXY2: Representam os valores das peças selecionadas no tabuleiro. São as saídas dos multiplexadores descritos na Etapa 5.
   - state3: Representa o estado do jogo em que ocorre a verificação de acerto, garantindo que a comparação só seja realizada na etapa correta e contabilize acerto apenas por um instante de pulso.
- <strong>Comparador</strong>
   - O comparador verifica a igualdade entre valueXY1 e valueXY2. e os valores forem iguais, a saída do comparador será ativada (lógica 1), indicando que as peças formar um par correto.
- <strong>Porta AND</strong>
   - A porta AND combina o resultado do comparador com o sinal do estado state3. Isso assegura que o pulso de "acerto" (correct) só será gerado se o jogo estiver no estado de verificação e os valores forem iguais.
- <strong> Saída: correct </strong>
   - A saída correct indica se o jogador acertou ao selecionar as peças. Este sinal é utilizado para atualizar a pontuação como vai ser descrito posteriomente.



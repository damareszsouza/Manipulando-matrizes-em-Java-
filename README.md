# Manipulando-matrizes-em-Java-

Ir para o conteúdo principal
 
Moodle - IFRS

Programação Básica com Java III - Turma 2022B
Painel Meus cursos  PBJIII2022B 3. Matrizes  3.4. Manipulando Matrizes
3.4. Manipulando Matrizes
Para acessar ou preencher uma posição de uma matriz bidimensional precisamos de dois índices. O processo é similar ao que fizemos para vetores, porém precisamos informar dois números separados por vírgula dentro dos colchetes (primeiro o número da linha e depois o da coluna). Por exemplo, se desejássemos acessar a posição presente na linha 2 e na coluna 1 de nosso tabuleiro do jogo da velha, escreveríamos:

tabuleiro[2, 1]
Em nosso algoritmo para o jogo da velha precisamos fazer com que a posição informada pelo jogador (linha e coluna) seja preenchida com o símbolo dele (X ou O). É claro que, antes de preencher a posição da matriz, precisamos nos certificar de que a posição seja válida, ou seja, que os números informados estejam no intervalo de 1 a 3 (nada que uma estrutura se...então não resolva). Assim, obtemos o algoritmo mostrado abaixo.




Algoritmo “Jogo da Velha”

var


jogador: caractere


linha, coluna: inteiro


tabuleiro: vetor [1..3, 1..3] de caractere;


inicio

       jogador ← ‘X’


enquanto condição faça


       escreva “Jogador ”, jogador, “ é a sua vez.”


       leia linha, coluna


      


       se linha >= 1 e linha <= 3 e coluna >= 1 e coluna <= 3 então              


tabuleiro[linha, coluna] ← jogador        


 


              se jogador = ‘X’ então


                    jogador ← ‘O’


       senão


                    jogador ← ‘X’


       fim se


 


       verificar se alguém ganhou


       senão


             escreva “Essa posição não existe!”


       fim se


fim enquanto


fim



O problema agora é verificar quando algum dos jogadores venceu ou quando houve empate. No jogo, alguém vence quando consegue completar três posições consecutivas no tabuleiro, em uma linha, coluna ou diagonal, como mostrado abaixo.

Possibilidades de vitória no jogo da velha. Para mais detalhes, ver legenda logo a seguir.

Legenda: Possibilidades de vitória no jogo da velha: a primeira mostra toda a primeira linha preenchida com X, a segunda mostra a segunda linha preenchida com X, a terceira mostra a terceira linha preenchida com X, a quarta mostra a primeira coluna preenchida com X, a quinta mostra a segunda coluna preenchida com X, a sexta mostra a terceira coluna preenchida com X, a sétima e a oitava mostram as diagonais preenchidas com X.



As possibilidades são as mesmas para o jogador O. A questão agora é: como construir uma sequência de instruções em nosso algoritmo para verificar todas essas possibilidades? É possível criar oito estruturas se...então, uma para cada possibilidade. Precisamos apenas verificar se existem valores iguais em linhas, colunas e diagonais. Esta solução gera o algoritmo mostrado abaixo. Criamos uma variável chamada vencedor, do tipo caractere, que conterá o valor ‘A’ se o jogo estiver em andamento, ‘X’ se o jogador X venceu, ‘O’ se o jogador O venceu e ‘E’ caso haja um empate.




se tabuleiro[1,1] = tabuleiro[1,2] e tabuleiro[1,2] = tabuleiro[1,3] então


                    vencedor ← tabuleiro[1,1]

       fim se

       se tabuleiro[2,1] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[2,3] então

                    vencedor ← tabuleiro[2,1]

       fim se

       se tabuleiro[3,1] = tabuleiro[3,2] e tabuleiro[3,2] = tabuleiro[3,3] então

                    vencedor ← tabuleiro[3,1]

       fim se

       se tabuleiro[1,1] = tabuleiro[2,1] e tabuleiro[2,1] = tabuleiro[3,1] então

                    vencedor ← tabuleiro[1,1]

       fim se

       se tabuleiro[1,2] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,2] então

                    vencedor ← tabuleiro[1,2]

       fim se

       se tabuleiro[1,3] = tabuleiro[2,3] e tabuleiro[2,3] = tabuleiro[3,3] então

                    vencedor ← tabuleiro[1,3]

       fim se

      se tabuleiro[1,1] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,3] então

                    vencedor ← tabuleiro[1,1]

      fim se

      se tabuleiro[1,3] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,1] então

                    vencedor ← tabuleiro[1,3]

      fim se



Esse código é grande! Será possível resumi-lo e gerar um algoritmo menor? Se analisarmos o código mostrado, veremos que os três primeiros se...então mostrados são praticamente iguais, mudando apenas o número das linhas utilizadas nos acessos às posições da matriz verificados. Nos três se...então seguintes temos uma situação similar, porém são os números das linhas que se mantém constantes e os números das colunas mudam. A mudança observada é uma variação de um a três. Assim, podemos utilizar estruturas para...faça para resumir essas instruções, como mostrado abaixo.




             para cont de 1 até 3 faça


se tabuleiro[cont,1] = tabuleiro[cont,2] e tabuleiro[cont,2] = tabuleiro[cont,3] então


                           vencedor ← tabuleiro[cont,1]


               fim se


             fim para

            para cont de 1 até 3 faça       


se tabuleiro[1,cont] = tabuleiro[2,cont] e tabuleiro[2,cont] = tabuleiro[3,cont] então


                           vencedor ← tabuleiro[1,cont]


              fim se


     fim para


      


     se tabuleiro[1,1] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,3] então


                    vencedor ← tabuleiro[1,1]

            fim se

            se tabuleiro[1,3] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,1] então


                    vencedor ← tabuleiro[1,3]

            fim se



Ainda é possível fazer mais uma melhoria em nosso algoritmo. Se observarmos as estruturas para...faça mostradas, podemos ver que elas são quase idênticas. Podemos fundi-las em uma única estrutura para...faça, sem modificar seu funcionamento, como mostrado abaixo.




             para cont de 1 até 3 faça


se tabuleiro[cont,1] = tabuleiro[cont,2] e tabuleiro[cont,2] = tabuleiro[cont,3] então


                           vencedor ← tabuleiro[cont,1]

                     fim se


              se tabuleiro[1,cont] = tabuleiro[2,cont] e tabuleiro[2,cont] = tabuleiro[3,cont] então


                           vencedor ← tabuleiro[1,cont]


              fim se


       fim para


      


se tabuleiro[1,1] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,3] então


                    vencedor ← tabuleiro[1,1]


       fim se


              se tabuleiro[1,3] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,1] então

                    vencedor ← tabuleiro[1,3]


       fim se



A versão final do algoritmo é mostrada abaixo. Note que incluímos também a condição no enquanto, para que o jogo continue enquanto não houver vencedor.




Algoritmo “Jogo da Velha”

var


jogador, vencedor: caractere


linha, coluna, cont, contaJogadas : inteiro


tabuleiro: vetor [1..3, 1..3] de caractere;


inicio

       jogador ← ‘X’

       vencedor ← ‘A’

       contaJogadas ← 0


enquanto vencedor != ‘X’ e vencedor != ‘O’ faça


       escreva “Jogador ”, jogador, “ é a sua vez.”


       leia linha, coluna


       se linha >= 1 e linha <= 3 e coluna >= 1 e coluna <= 3 então              


tabuleiro[linha, coluna] ← jogador        


              se jogador = ‘X’ então


                    jogador ← ‘O’


       senão


                    jogador ← ‘X’


       fim se


       contaJogadas ← contaJogadas + 1


       se contaJogadas = 9 então


             vencedor ← ‘E’


       fim se


 


             para cont de 1 até 3 faça


se tabuleiro[cont,1] = tabuleiro[cont,2] e tabuleiro[cont,2] = tabuleiro[cont,3] então


                           vencedor ← tabuleiro[cont,1]


                     fim se


             se tabuleiro[1,cont] = tabuleiro[2,cont] e tabuleiro[2,cont] = tabuleiro[3,cont] então


                           vencedor ← tabuleiro[1,cont]


             fim se

       fim para



      


se tabuleiro[1,1] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,3] então


                    vencedor ← tabuleiro[1,1]


       fim se


              se tabuleiro[1,3] = tabuleiro[2,2] e tabuleiro[2,2] = tabuleiro[3,1] então


                    vencedor ← tabuleiro[1,3]


       fim se


       senão


             escreva “Essa posição não existe!”


       fim se


fim enquanto

fim



Veja que incluímos no algoritmo uma verificação de empate.  Para isso contamos o número de jogadas efetuadas. Caso tenham sido efetuadas nove jogadas e não houve vencedor, haverá um empate e a letra E será atribuída à variável vencedor.

Este algoritmo ainda não está totalmente completo. Resta-nos incluir código para mostrar quem foi o vencedor ou se houve empate. Deixamos essa parte momentaneamente como exercício ao leitor, porém mostraremos o código em Java para isso na próxima seção.

Última atualização: domingo, 1 nov 2020, 19:13
Seguir para...
Academi
Dúvidas? 
Perguntas frequentes

Fale conosco | Suporte | Contato

Informação
Termos e Condições de Uso
Aviso de Privacidade e Proteção de Dados Pessoais
Contato
Rua Gen. Osório, 348, Bento Gonçalves/RS
Siga-nos
Copyright © 2017 - Desenvolvido por LMSACE.com. Distribuído por Moodle

Português - Brasil ‎(pt_br)‎
English ‎(en)‎
Español - Internacional ‎(es)‎
Français ‎(fr)‎
Italiano ‎(it)‎
Português - Brasil ‎(pt_br)‎
Mudar para o tema padrão

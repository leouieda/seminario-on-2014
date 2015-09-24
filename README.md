# Modelagem e inversão em coordenadas esféricas na gravimetria

[Leonardo Uieda](http://www.leouieda.com)

Seminário anual (2014) da pós-graduação em geofísica do Observatório Nacional.

Slides at [SpeakerDeck](https://speakerdeck.com/leouieda/modelagem-e-inversao-em-coordenadas-esfericas-na-gravimetria).


## Resumo

Os métodos lineares de inversão 3D na gravimetria
geralmente discretizam a Terra
em prismas retangulares retos homogêneos.
O problema inverso consiste
em estimar uma distribuição de densidade dos prismas
que ajuste a anomalia da gravidade medida.
No entanto,
em estudos de modelagem
de escala regional ou global
é desejável levar em conta
a curvatura da Terra.
Uma abordagem para isso
é discretizar a Terra em prismas esféricos,
também chamados de tesseroides.
Assim,
métodos existentes de inversão
em coordenadas Cartesianas
utilizando prismas retangulares
podem ser adaptados
para usar tesseroides
em coordenadas esféricas.
Em geral,
esta adaptação requer
um método para calcular
o efeito gravitacional de um tesseroide
com precisão
e um software que implemente
tanto o cálculo direto
quanto o método de inversão.

O potencial gravitacional e suas derivadas
causados por um tesseroide
não possuem soluções analíticas.
Foram propostos dois métodos para a integração numérica:
a Quadratura Gauss-Legendre
e a expansão do integrando em série de Taylor.
A Quadratura Gauss-Legendre
consiste em aproximar a integral
por uma soma ponderada
do efeito gravitacional de N massas pontuais.
Essas massas pontuais
são colocadas em pontos
no interior do tesseroide
que correspondem a raízes
de um polinômio de Legendre de grau N.
O número de massas utilizadas (N)
é chamado de ``ordem'' da quadratura.
A acurácia da integração numérica
depende do número de massas utilizadas
e da distância do tesseroide ao ponto de observação.
Quanto mais próximo estiver o ponto de observação,
mais massas serão necessárias.
Este comportamento
pode ser justificado
do ponto de vista da teoria da amostragem.
É conhecido em métodos potenciais
que quanto mais próximo for o ponto de observação,
maior é a frequência espacial (número de onda)
do campo potencial.
Consequentemente,
na integração numérica são necessários
mais pontos para discretizar o integrando
sem que ocorra falseamento.

Um método proposto na literatura
para aumentar o número de massas pontuais
sem aumentar a ordem da quadratura
é dividir o tesseroide em tesseroides menores.
O campo calculado
é a soma dos campos dos tesseroides menores,
que são calculados
com um número fixo de massas.
Esta divisão se repete
para cada tesseroide menor
até que ponto de observação
esteja distante o suficiente
em relação ao tamanho do tesseroide.
Desta forma,
o número de divisões,
e consequentemente o número de massas pontuais,
é maior nas partes do tesseroide
próximas do ponto de observação.
Podemos dizer que
a acurácia da integração numérica
depende da razão entre
a distância até o ponto de observação
e o tamanho do tesseroide.
Trabalhos anteriores
sugerem que esta razão
deve ser próxima de 1 (um).
Porém,
atualmente não há uma análise
que relacione quantitativamente
a maior razão distância/tamanho permitida
com o erro cometido na integração.

Neste trabalho,
investigamos qual é o erro
cometido na integração numérica
com divisão automática dos tesseroides.
Utilizamos como referência
o modelo de uma casca esférica,
para qual existe
uma solução analítica.
Esta casca é discretizada em tesseroides.
Comparamos o potencial gravitacional
e suas primeiras e segundas derivadas
calculados a partir do modelo de tesseroides
com o valor equivalente
para a casca esférica.
Este cálculo foi feito
para diversos valores
da máxima razão distância/tamanho permitida.
Fizemos um gráfico
do erro cometido na integração
em função da razão distância/tamanho.
Desta forma,
determinamos qual é o valor desta razão
que proporciona um erro máximo aceitável.
Esta análise pode ser feita
para o potencial gravitacional e suas derivadas.

Utilizamos os resultados acima
para adaptar o método de inversão de ``plantação de densidades''
a coordenadas esféricas.
Este método utiliza
um algoritmo de busca sistemática
para construir a solução do problema inverso.
O algoritmo adiciona tesseroides
em torno de um conjunto inicial
de tesseroides ``sementes''
fornecidos pelo interprete.
A solução cresce
em torno das sementes
até que os dados preditos pela solução
ajustem os dados observados.
A maior vantagem do método de plantação
é sua eficiência computacional.
O algoritmo não requer
a solução de sistemas lineares
e a matriz de sensibilidade
pode ser calculada de forma eficiente.
Realizamos testes
com dados sintéticos
tanto da anomalia da gravidade
como do tensor gradiente da gravidade.

A modelagem direta com tesseroides
e a inversão por algoritmo de plantação
foram implementadas no software livre
Fatiando a Terra ([www.fatiando.org](http://www.fatiando.org)).
Recentemente,
desenvolvemos um novo módulo
chamado `fatiando.inversion`.
Este módulo
automatiza grande parte
da criação de um problema inverso.
Para implementar um problema novo,
o usuário necessita somente desenvolver
a solução do problema direto
e a criação da matriz de sensibilidade.
Uma vez feitas essas duas etapas,
o usuário tem acesso automático
a diversos métodos de optimização e regularização.
As rotinas de modelagem direta
implementadas no Fatiando a Terra
podem ser reutilizadas
para desenvolver novos métodos de inversão
e adaptar métodos existentes a novas parametrizações.

Em conclusão,
determinamos um valor ideal
para a razão entre a distância ao ponto observação
e o tamanho de um tesseroide
através da comparação
com o efeito de uma casca esférica.
Esta razão é utilizada
em um algoritmo de divisão automática dos tesseroides
para garantir que o erro na integração numérica
seja menor que um valor estabelecido.
Observamos que o valor ideal
para a razão distância/tamanho
é diferente para o potencial
e suas derivadas segundas.
Esses resultados foram utilizados
na adaptação para coordenadas esféricas
do método de inversão por plantação de densidades.
Esta adaptação foi testada
em dados sintéticos
que simulam diferentes ambientes geológicos.
Para a aplicação em dados reais,
serão utilizados dados de modelos geopotenciais.
Também investigaremos
a utilização dos dados de gravimetria da gravidade
fornecidos pelo satélite GOCE.
O código para gerar este resumo
e a apresentação que o acompanha
está disponível em
[github.com/leouieda/seminario-on-2014](https://github.com/leouieda/seminario-on-2014).

## License

[![Creative Commons
License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)
This work is licensed under a
[Creative Commons Attribution 4.0 International
License](http://creativecommons.org/licenses/by/4.0/).

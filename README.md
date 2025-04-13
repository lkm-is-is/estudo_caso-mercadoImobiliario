# estudo_caso-mercadoImobiliario
Um projeto que analisa o mercado imobiliário brasileiro. O dataset deriva de dados do ZAP Imóveis, em 2022, maior portal de anúncios de imóveis em atividade no país.


Fontes: https://github.com/ziggy-data/scraping_zap_imoveis
data-ap-geral

Este é um estudo de caso de anúncios de apartamentos da ZAPImóveis datado de 2022. O dataset foi obtido do repositório público: "scraping_zap_imoveis" by Reinaldo A Simoes @ziggy-data.
Primeiro, realizou-se análise exploratória e pré-processamento de dados. Através de investigações preliminares, a amostra foi segmentada em apartamento até 100m2, sem outliers de preço/m2. 
Essa amostra final segmentada foi utilizada para realizar testes de Regressão Linear Múltipla.

**************
**************

RESULTADOS

=== DADOS LIMPOS ===
Registros válidos: 6682/6709
Faixa de valores: R$110,000.00 - R$1,420,000.00


=== ESTATÍSTICAS DAS VARIÁVEIS ===
          area(m2)     banheiro      garagem      quartos        suite
count  6682.000000  6682.000000  6682.000000  6682.000000  6682.000000
mean     64.603562     1.551931     1.125711     2.122418     0.297366
std      16.358206     0.650893     0.634110     0.576943     0.457133
min      26.000000     1.000000     0.000000     1.000000     0.000000
25%      51.000000     1.000000     1.000000     2.000000     0.000000
50%      63.000000     1.000000     1.000000     2.000000     0.000000
75%      76.000000     2.000000     1.000000     2.000000     1.000000
max     100.000000     7.000000    22.000000     4.000000     1.000000


=== VALORES ÚNICOS ===
area(m2): [np.int64(26), np.int64(27), np.int64(28), np.int64(29), np.int64(30), np.int64(31), np.int64(32), np.int64(33), np.int64(34), np.int64(35), np.int64(36), np.int64(37), np.int64(38), np.int64(39), np.int64(40), np.int64(41), np.int64(42), np.int64(43), np.int64(44), np.int64(45), np.int64(46), np.int64(47), np.int64(48), np.int64(49), np.int64(50), np.int64(51), np.int64(52), np.int64(53), np.int64(54), np.int64(55), np.int64(56), np.int64(57), np.int64(58), np.int64(59), np.int64(60), np.int64(61), np.int64(62), np.int64(63), np.int64(64), np.int64(65), np.int64(66), np.int64(67), np.int64(68), np.int64(69), np.int64(70), np.int64(71), np.int64(72), np.int64(73), np.int64(74), np.int64(75), np.int64(76), np.int64(77), np.int64(78), np.int64(79), np.int64(80), np.int64(81), np.int64(82), np.int64(83), np.int64(84), np.int64(85), np.int64(86), np.int64(87), np.int64(88), np.int64(89), np.int64(90), np.int64(91), np.int64(92), np.int64(93), np.int64(94), np.int64(95), np.int64(96), np.int64(97), np.int64(98), np.int64(99), np.int64(100)]
banheiro: [np.int64(1), np.int64(2), np.int64(3), np.int64(4), np.int64(5), np.int64(7)]
garagem: [np.int64(0), np.int64(1), np.int64(2), np.int64(3), np.int64(4), np.int64(22)]
quartos: [np.int64(1), np.int64(2), np.int64(3), np.int64(4)]
suite: [np.int64(0), np.int64(1)]


=== VERIFICAÇÃO DE MULTICOLINEARIDADE ===
...
0  area(m2)            1.4%   + 1.4%        1.4% por m² adicional
3   quartos           -6.4%    -6.4%   -6.4% por quarto adicional

Valor base (imóvel 0m²): R$103,507.92 (intercepto exponenciado)


=== VERIFICAÇÃO DE RESÍDUOS ===
Média dos resíduos: R$29,288.34 (deve ser próxima de zero)
Assimetria: 0.86 (ideal entre -0.5 e 0.5)


=== EXEMPLOS DE PREDIÇÃO ===
Exemplo 1 (70m², 2 quartos, COM suíte): R$462,488.56
Exemplo 2 (70m², 2 quartos, SEM suíte): R$437,307.24

=== ANÁLISE DE CORRELAÇÃO ===
valor       1.000000
area(m2)    0.644305
banheiro    0.612146
garagem     0.410182
quartos     0.343801
suite       0.267211
Name: valor, dtype: float64


********************************************
*********************************************

Dados Limpos
6682 registros válidos de um total de 6709: excelente taxa de dados limpos.
Faixa de valores dos imóveis: de R$110 mil a R$1,42 milhão.

Estatísticas das Variáveis
Área (m²) Média: 64,6 m²
50% dos imóveis têm até 63 m²
Máximo: 100 m²

Banheiros Média: 1,55
75% dos imóveis têm até 2 banheiros

Garagem Média: 1,13 vagas
75% têm 1 vaga

Quartos Média: 2,12
A maioria tem 2 quartos
Máximo de 4 quartos

Suíte Média: 0,3, ou seja, menos de 1/3 dos imóveis têm suíte


Multicolinearidade
O modelo identificou que:
A área tem +1,4% de impacto por m² adicional no valor do imóvel.
Cada quarto adicional reduz o valor estimado em -6,4%. Isso é contraintuitivo e pode indicar: Correlação espúria (ex: apts maiores com mais quartos em regiões mais baratas); Problema com o modelo (colinearidade ou codificação errada).
Valor base estimado: R$103.507,92 para um imóvel com 0 m² (intercepto do modelo exponenciado). Serve só como referência matemática.


Verificação de Resíduos
Média dos resíduos = R$29.288,34, o que não é próximo de zero — pode indicar:
Tendência sistemática de superestimar ou subestimar os preços.
Assimetria = 0.86: os resíduos são assimétricos à direita, ou seja, o modelo frequentemente subestima os valores altos.

Exemplos de Predição
Imóvel de 70m² com 2 quartos:
Com suíte: R$462.488,56
Sem suíte: R$437.307,24

A diferença entre ter ou não suíte é de cerca de R$25 mil.

Correlação com o valor
Variável	      Correlação
Área	          0.64 (forte)
Banheiro	      0.61 (forte)
Garagem	        0.41 (moderada)
Quartos	        0.34 (fraca/moderada)
Suíte	          0.26 (fraca)

O valor é mais influenciado pela área e pelo número de banheiros do que pelo número de quartos ou pela presença de suíte.

Considerações finais
O modelo tem boa aderência geral, mas: Pode estar superficial em capturar nuances de localização; Há sinais de multicolinearidade (quartos com peso negativo); Os resíduos e a assimetria indicam que o modelo precisa de refinamento, talvez com: Transformações logarítmicas; Segmentação por clusters geográficos.


***************************************************
LIMITAÇÃO DOS DADOS GEOGRÁFICOS
Talvez seja necessário incluir a localização como um fator relevante na relação de valor do apartamento. No entanto, os dados possuem significados diferentes, ora referenciando cidades ora bairros. 
Uma análise mais apurada necessita de uma identificação por Estado, por exemplo, através de agrupamentos. (Uso de alguma API com dados geográficos do Brasil?). Ou então categorizações: capital, interior, etc.



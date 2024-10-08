# aps4_cdados

# APS 4 - Observando Eventos Independentes

## Introdução

Até o momento, estudamos dois modelos estatísticos: o modelo Binomial e o modelo Poisson. Os dois modelos são semelhantes nos seguintes sentidos:

1. Servem para contar sucessos em uma sequência de experimentos (ex: jogadas de moeda em que sai "Cara")
2. Os experimentos analisados são independentes entre si
3. A probabilidade de sucesso de um experimento é constante e igual a $p$.

A diferença entre os modelos Binomial e Poisson está no tipo de informação que usamos.

No modelo *Binomial*, sabemos exatamente o número de experimentos ($n$) e esperamos uma quantidade $k=np$ de sucessos. Nesse caso, temos acesso tanto ao número de experimentos quanto ao número de sucessos, e podemos usar essas informações para estimar $p$.

No modelo $Poisson$, o número de experimentos tende a infinito, e a probabilidade de sucesso tende a zero, e forma que $np=\lambda$ é uma constante. Então, só temos acesso ao número de sucessos, não ao número de experimentos. Nos modelos *Poisson*, somente estimamos o valor de $\lambda$, mas não sabemos exatamente os valores de $n$ ou $p$.

Em ambos os casos, podemos usar o processo de modelagem para fazer inferências sobre o comportamento de grupos. Por exemplo:

### Atuação do Ronaldo Fenômeno no Corinthians em 2009

No campeonato paulista de 2007, o Corinthians pontuou (ganhou ou empatou) em 13 dos 19 jogos. Buscando melhorar sua campanha, no fim de 2008 o clube contratou o jogador Ronaldo (R9 / fenômeno). Em 2009, o Corinthians pontuou (ganhou ou empatou) em 19 dos 19 jogos. Será que a campanha com atuação do Ronaldo foi realmente diferente, ou foi só uma flutuação natural dos dados?

Para isso, vamos supor que cada jogo é independente, e em cada jogo o Corinthians tem uma probabilidade $p$ de pontuar.

Vamos agora assumir a hipótese de que a probabilidade $p$ de pontuar é igual em 2007 e 2009. Vamos assumir que a campanha de 2007 é o status quo, ou seja, existia um Corinthians sem impacto nenhum do Ronaldo em 2007.

Se estimamos $p$ com base na campanha de 2007, então $p=13/19=0.684$. Nesse caso, a probabilidade de encontrarmos uma campanha com 19 jogos e 19 vitórias pode ser calculada pela `cdf` de uma distribuição binomial: `1-st.binom.cdf(n=19, k=18, p=p)`, obtendo $0.0007$. Esse número é muito baixo, indicando que a campanha de 2009 é realmente diferente da campanha de 2007, ao menos em relação ao número de jogos em que o time pontuou.

### A Final da Copa do Mundo de 94

A final da copa do mundo de 1994 foi disputada entre Brasil e Itália e foi resolvida numa disputa de pênaltis. Na disputa, o Brasil marcou gol em 3 de 4 jogadas, e a Itália marcou em 2 de suas 5 tentativas. Será que essa diferença mostra que houve uma diferença nos treinamentos das equipes, ou trata-se de uma flutuação natural, que pode acontecer em qualquer jogo?

Vamos supor que as cobranças de Brasil e Itália são independentes, e que ambos têm probabilidade $p$ de marcar gols.

Vamos estimar $p$ usando os dados do Brasil: $p=3/4=0.75$. Nessas condições, podemos calcular a probabilidade de a Itália marcar 2 ou menos gols em 5 jogadas usando a `cdf`: `st.binom.cdf(n=5, k=2, p=0.75)`, obtendo $0.10$. Veja, se os treinamentos fossem estritamente iguais, esse desempenho da itália ainda teria 10% de chance de acontecer.

### Enunciado da atividade

Nesta atividade, você vai escolher algum fenômeno à sua volta que possa ser observado em duas condições diferentes, e verificará se pode dizer seguramente que há diferenças no fenômeno em cada uma das condições. O fenômeno deve poder ser modelado por uma distribuição Binomial ou Poisson. Por exemplo (esses já não valem):

* Será que menos pessoas almoçam no 5o. andar do P1 às sextas que no restante dos dias? (Fenômeno = número de pessoas almoçando, modelo = Poisson)
* Será que passam mais carros na Hélio Pelegrino em dias de chuva que em dias de Sol? (Fenômeno = número de carros que passam, modelo = Poisson)
* Será que há alguma disciplina em que o índice de reprovação foi maior que outras? (Fenômeno = número de pessoas reprovadas, modelo = Binomial)
* Será que há mais pessoas tomando café com açúcar ou sem açúcar? (Fenômento = número de pessoas que tomam café sem açúcar, modelo = Binomial)

Para isso, siga os seguintes passos:

1. Escolha um fenômeno à sua volta ou a que você tenha acesso e explique porque ele pode ser modelado por uma Binomial ou por Poisson (escolha a distribuição!!!). Em especial, explique quais fenômenos são *independentes entre si.*
2. Escolha duas situações em que o fenômeno aconteça e que possam ser observadas, e justifique porque deveria haver alguma diferença entre elas.
3. Colete dados sobre seu fenômeno, nas duas situações. Se não achar dados, ou julgar que não conseguirá coletá-los em tempo hábil, guarde essa ideia para depois, volte ao passo 1 e escolha outro fenômeno.
4. Estime os parâmetros do modelo usando dados de uma das situações.
5. Após, estime a probabilidade de encontrar os dados tão ou mais extremos quanto os dados da outra situação.
6. Com base nos resultados do ítem anterior, decida se é seguro dizer que as duas situações escolhidas levam a comportamentos diferentes do seu fenômeno.

## Sobre o uso de IA (ChatGPT, etc.)

ChatGPT e outros modelos de linguagem são ferramentas de produtividade importantes e relevantes. Por outro lado, seu uso indiscriminado pode se tornar um ruído no processo de produção e feedback das atividades, pelos seguintes motivos:

1. O texto produzido é um *proxy* para o entendimento do aluno. Analisando o texto, queremos entender quais são os *gaps* de aprendizado que acontecem, de forma que possamos planejar intervenções pertinentes.
2. O feedback fornecido parte do pressuposto de que o texto foi o melhor trabalho possível apresentado pelo aluno. Nesse contexto, o *feedback* tem a intenção de revisar e proporcionar ao aluno uma visão externa com o intuito de melhorar ou refinar sua compreensão e sua expressão sobre o tema. Fornecer *feedback* para um texto gerado por máquina não tem esse efeito, porém é tão ou mais trabalhoso que dar *feedback* para textos feitos por humanos.

Pensando nisso, vamos adotar as seguintes regras para o uso de ChatGPT e IAs generativas de forma geral para a redação de textos:

1. Caso o grupo decida usar ChatGPT ou equivalente para qualquer parte de sua redação, deve **obrigatoriamente** adicionar uma nova seção anexa ao relatório em que mostra todos os prompts e respostas do ChatGPT (ou todas as interações equivalentes).
2. Também, para cada trecho que use IA, o grupo deverá **explicitamente** justificar porque o trecho foi considerado correto. Justificativas vagas como "achamos pertinente", "condiz com a matéria", etc., não serão aceitas. Justificativas válidas são aquelas que associam explicitamente o texto fornecido pela IA a uma equação, observação ou raciocínio pertinentes ao texto.
3. Neste anexo citado e nas justificativas, não é permitido usar nenhum tipo de IA.
4. O uso de IA sem a citação adequada ou sem o anexo (qualquer um deles, ou ambos simultaneamente), se detectado, será considerado como cópia sem citação de fonte, e, portanto, violação do código de ética.

# Entregas esperadas

Você deve entregar, via Blackboard, um arquivo PDF (uma entrega por grupo!) contendo:

1. Nome do grupo
2. Título do trabalho, que deve ser algo como "Fenômeno X (seu fenômeno escolhido) nas situações A e B usando modelo (seu modelo)" (parafraseie isso!)
3. Um texto explicando todos os ítens do desenvolvimento com detalhe suficiente para permitir que alguém de outra turma desta disciplina possa reproduzir o mesmo experimento e criticá-lo.
4. Uma auto-avaliação da do texto, justificando a nota que foi auto-atribuídas.

# Rubricas e avaliação

Cada um dos ítens (exceto a auto-avaliação) será avaliado da seguinte forma:

| Rubrica | Descrição                                                                                                                                                                                                                                                                                                                                                            | Exemplo                                                                                                                                                              |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| F       | Não entregue, entregue fora do prazo, entregue fora do escopo ("fiz outra coisa")                                                                                                                                                                                                                                                                                     | Não entregar                                                                                                                                                        |
| E       | Entregue no prazo e dentro do escopo, mas a entrega tem um ou mais ítens faltando ou só é compreensível se for acompanhado deste enunciado (por exemplo, ao dizer "resposta ao ítem 2" ao invés de ter um título explicativo) ou está ilegível (exemplo: textos sem sentido ou figuras muito grandes / muito pequenas ou em resolução baixa)                | Colocar no título de uma figura: "ítem 1a"                                                                                                                         |
| D       | A entrega tem falhas graves de coesão ou coerência que impedem sua compreensão, ou faltam elementos essenciais (título, legenda, rótulos nos eixos), ou o texto deixa de indicar o que são ideias originais e o que são ideias retiradas de outras fontes, ou as ideias/dados são mostrados de forma embaralhada, sem guiar o leitor a um fluxo de pensamento. | Em um texto: "Existe impacto da renda na educação. Isso porque a renda pode estar ligada a condições de estudo. O estudo é essencial para formar seres humanos" |
| C       | A entrega não tem falhas graves. Todas as fontes de ideias são indicadas. A entrega traz ao menos um elemento errado ou ao menos um elemento supérfluo (que não contribui para a mensagem passada).                                                                                                                                                                | Em um texto: "Essa é uma fonte de 100W (Watts, unidade batizada em homenagem a James Watt, inventor da máquina a vapor")                                           |
| B       | A entrega tem todos os elementos necessários para passar a mensagem, a mensagem é clara, e não há elementos supérfluos.                                                                                                                                                                                                                                           | Título da figura: "Média de desempenho no ENEM 2022 por disciplina por faixa de renda", com rótulo no eixo Y: "Pontos" e rótulo no eixo X: "faixa de renda".     |
| A       | A entrega está correta e o conteúdo mostra ou induz uma análise crítica do contexto ou das implicações dos dados e informações coletadas.                                                                                                                                                                                                                      | Título da figura: "Desempenho no ENEM diminui com o aumento da renda", com rótulo no eixo Y: "Pontos" e rótulo no eixo X: "faixa de renda".                       |

A auto-avaliação será avaliada da seguinte forma:

| Rubrica | Descrição                                                                                                                                                                                  | Exemplo                                                                                                                                                                                                                                               |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| F       | Não entregue, entregue fora do prazo, entregue fora do escopo ("fiz outra coisa")                                                                                                           | Não entregar                                                                                                                                                                                                                                         |
| D       | Entregue no prazo e dentro do escopo, mas somente copia as rubricas que foram apresentadas, sem relacioná-las com o material apresentado, ou apresenta notas sem argumentar o motivo delas. | "Nota A, pois está correto e o conteúdo induz análise crítica do contexto"                                                                                                                                                                        |
| C       | Entregue, mas claramente puxa as notas "para cima" ou "para baixo" sem ter argumentos                                                                                                        | Entrega é uma figura sem título, mas auto-avaliação diz: "o título da figura está correto"                                                                                                                                                      |
| A       | Entregue, e argumentado corretamente                                                                                                                                                         | "Nota A porque a passagem `de acordo com Fulano et al.` mostra que os resultados obtidos condizem com a literatura", ou "Nota B, porque a figura tem todos os elementos, embora não tenha nenhuma indicação de uma leitura crítica do contexto. |

Para atingir cada nível, é necessário cumprir todos os requisitos do nível anterior. Cada uma das entregas será avaliada individualmente e isoladamente. A nota geral do trabalho será a **menor** entre as notas das entregas.

Caso haja interações com IAs, elas serão avaliadas de acordo com a seguinte rubrica:

| Rubrica           | Descrição                                                                                                                                                                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Código de ética | Foi identificado o uso de Inteligência Artificial, mas o texto não demonstra clara e diretamente que uma ferramenta foi utilizada ou como ela foi utilizada.                                                                                                            |
| F                 | Somente colocou o enunciado da atividade como entrada da IA e fez alterações mínimas no resultado apresentado. Toda ou a maior parte da informação relevante do trabalho foi gerada pela IA.                                                                        |
| E                 | Trouxe tópicos específicos à IA, mas as conexões lógicas foram todas ou em sua maioria trazidas pela IA. OU: Uma ou mais informações inventadas pela IA (alucinações) foram transportadas para o texto sem crítica.                                             |
| D                 | O grupo trouxe alguns elementos relevantes para a IA, mas todas ou a maioria das conexões lógicas foram feitas pela própria IA.                                                                                                                                        |
| C                 | O grupo trouxe a maioria dos elementos relevantes para a IA, mas a IA ainda foi responsável por trazer ao menos um elemento essencial ao trabalho.                                                                                                                       |
| B                 | IA foi usada para frasear raciocínios, mas todos os elementos relevantes para a construção dos raciocínios foram fornecidas pelo grupo de trabalho.                                                                                                                   |
| A                 | IA foi usada apenas para correções estilísticas, e todo o conteúdo relevante e todas as linhas de raciocínio foram feitas pelo grupo de trabalho, OU a IA foi usada somente para obter ideias sobre o assunto e o grupo escreveu todo o conteúdo com suas palavras. |
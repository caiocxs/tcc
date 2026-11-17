# Roteiro de falas — Defesa TCC2 (alvo: ~20 minutos)
## Capa (~15s)
**No TCC:** folha de rosto (título, autor, orientador, coorientador).
**No slide:** título completo do TCC, nome, instituição, orientador/coorientador, "São Paulo, 2026".

**Fala sugerida:**
"Boa tarde. Meu nome é Caio Xavier da Silva, e esta é a defesa do meu Trabalho de Conclusão de Curso: análise estática generativa com LLMs, otimizando a detecção de vulnerabilidades no SemGrep via uma abordagem multi-agente."

## Roteiro da apresentação (~15s)
**No TCC:** corresponde ao Sumário do documento (os quatro capítulos: Introdução, Revisão Bibliográfica, Desenvolvimento, Conclusão).
**No slide:** `\tableofcontents` — lista as cinco seções da apresentação: Problema e motivação / Ferramentas utilizadas / Objetivos e método / Resultados / Conclusão.

**Fala sugerida:**
"Vou seguir cinco blocos: o problema e a motivação, uma breve apresentação das ferramentas que uso, os objetivos e o método, os resultados — que é onde vou passar a maior parte do tempo — e a conclusão."

---

## 1. Problema e motivação

### Slide: O problema (~1,5 min)
**No TCC:** Capítulo 1 — Introdução, abertura do capítulo, antes da Seção 1.1 (p. 11-12); e Seção 1.1 "Contextualização do problema" (p. 13-17).
> "Em 2014, a ausência de uma única verificação de tamanho em uma rotina de manipulação de memória da biblioteca OpenSSL[...] deu origem à vulnerabilidade conhecida como *Heartbleed* (CVE-2014-0160)." (Cap. 1, p. 11)
> "A falha permitia que qualquer pessoa lesse trechos da memória dos servidores afetados, expondo senhas, dados pessoais e chaves criptográficas." (Cap. 1, p. 11)
> "Estima-se que, no momento da divulgação, entre 24% e 55% dos servidores HTTPS do milhão de *sites* mais acessados do mundo estavam vulneráveis." (Cap. 1, p. 11)
> "A Microsoft relata que cerca de 70% das vulnerabilidades[...] são problemas de segurança de memória[...] cerca de 70% eram problemas de segurança de memória, e metade destas, do tipo uso de memória após a sua liberação." (Cap. 1, p. 11)
> "Pesquisas revelam que menos de 5% das lógicas de detecção utilizadas na indústria são criadas por usuários comuns." (Tabela 1 — *Limitações da análise estática tradicional*, p. 12, linha "Esforço Humano")
> "Estudos empíricos confirmam que essa abordagem pode consumir dezenas de milhões de *tokens* e exigir dias de processamento contínuo [...] Essa sobrecarga de contexto exacerba o risco de alucinações." (Seção 1.1, p. 16)

**Fala sugerida:**
- Para dimensionar o problema

- Em 2014, CVE do OpenSSL deu origem ao Heartbleed.

- Na prática, essa falha permitia que qualquer pessoa, de fora, lesse pedaços da memória do servidor afetado como: senhas, dados pessoais e até as chaves criptográficas usadas para proteger a comunicação.

- O caso mais documentado de dano real foi o da Receita Federal do Canadá, que confirmou publicamente o roubo de dados fiscais de contribuintes através dessa falha.

- Cerca de 70% das vulnerabilidades críticas da Microsoft, e uma proporção parecida no Chromium, são erros de segurança de memória.

- Conclusão:
    - O problema é que a análise estática tradicional depende de regras escritas à mão, e menos de 5% das lógicas de detecção usadas na indústria são criadas por usuários comuns, porque exige conhecimento muito especializado. 

- Uma alternativa seria jogar o código inteiro para um LLM.
    - Custo de dezenas de milhões de tokens, dias de processamento, e traz risco de alucinação.

### Slide: Pergunta de pesquisa (~1,5 min)
**No TCC:** Seção 1.2 "Formulação do problema" (p. 17-18).
> "Um *framework* multi-agente baseado em LLMs é capaz de sintetizar regras para o SemGrep que detectem vulnerabilidades em código C com *recall* e precisão estatisticamente superiores aos do *ruleset* tradicional da ferramenta?" (citação direta, Seção 1.2, p. 17)
> "O escopo restringe-se à linguagem C, a cinco categorias de CWE [...] e ao SemGrep como motor de execução das regras." (Seção 1.2, p. 18) — a lista e definição das cinco CWEs está na Seção 2.2.2.2 "*Common Weakness Enumeration*" (p. 32, referencial teórico, fora do escopo dos 15 min).

**Fala sugerida:**
- Concluindo para a pergunta central do trabalho:
    - [Slide]
    - Com recall e precisão estatisticamente superiores ao ruleset tradicional.

- Com o seguinte escopo e CWEs;

---

## 2. Ferramentas utilizadas

### Slide: Ferramenta: SemGrep (~1 min)
**No TCC:** Seção 1.1 "Contextualização do problema" (p. 17) — introdução breve, no fechamento da seção; e Seção 2.2.1.6 "Análise estática baseada em regras" (p. 29-30, referencial teórico) — definição técnica completa.
> "O SemGrep é uma ferramenta de código aberto na qual o usuário descreve, em arquivos no formato YAML, regras cujos padrões imitam a própria sintaxe da linguagem analisada." (Seção 1.1, p. 17)
> "O SemGrep disponibiliza um *ruleset* oficial [...] neste trabalho, é a esse conjunto que se refere a expressão *ruleset* tradicional." (Seção 1.1, p. 17)
> "Formalmente, SemGrep é uma ferramenta de análise estática que suporta estruturas complexas e verificações básicas de fluxo de dados no código, permitindo inspeções sem execução [...] para identificar vulnerabilidades de segurança." (Seção 2.2.1.6, p. 29)
> "SemGrep converte código em uma árvore de sintaxe abstrata universal (UAST), aplicando um *pattern-matching* uniforme em mais de 30 linguagens." (Seção 2.2.1.6, p. 30)
> "Metavariáveis [...] são atribuídas quando SemGrep identifica um padrão que se encaixa [...] se a metavariável é reutilizada na mesma regra, o SemGrep exigirá que o valor capturado seja exatamente o mesmo, o que permite *Data Flow*." (Seção 2.2.1.6, p. 30)
> "Ellipsis/Curinga (...), representando qualquer sequência de coisas [...] tornando SemGrep uma ferramenta abstraída." (Seção 2.2.1.6, p. 30)

**Fala sugerida:**
- O SemGrep é um analisador estático de código aberto. 
    - A regra é escrita em YAML, e o padrão dela imita a própria sintaxe da linguagem analisada.
    - Diferente do CodeQL, por exemplo, que trata o código como um banco de dados relacional, com sua própria linguagem.

- Por trás dos panos, ele converte o código numa árvore de sintaxe universal, o que permite rodar o mesmo motor de busca em mais de 30 linguagens diferentes.

- Dois recursos são centrais: a metavariável, que captura um valor e exige que, se reaparecer na regra, seja exatamente o mesmo — é assim que ele enxerga fluxo de dados.
- E as reticências, que deixam ignorar qualquer trecho irrelevante no meio do padrão.

- A ferramenta contém um modo *taint*: declara-se uma fonte de contaminação, e se rastreia o fluxo de dados ao invés de procurar padrões sintáticos isolados.

- E uma última coisa importante: o SemGrep tem um conjunto de regras público, de várias CWEs de diversas linguagens, mantido pela comunidade, é esse conjunto que será nossa "regras tradicionais".

### Slide: Exemplo de regra SemGrep (~30s)
**No TCC:** Seção 1.1 "Contextualização do problema" (p. 17-18), Figura 3 "*Exemplo de regra criada para detectar uma senha embutida no argumento da função em Python*".
> "O SemGrep é uma ferramenta de código aberto na qual o usuário descreve, em arquivos no formato YAML, regras cujos padrões imitam a própria sintaxe da linguagem analisada, como ilustra a Figura [3]." (Seção 1.1, p. 17)
> Legenda da figura: "Fonte: Adaptado para português com finalidade de melhorar compreensão (Hou et al., 2025)."

**Fala sugerida:**
- É exatamente esse tipo de regra, só que em C e para os CWEs de memória, que o nosso framework gera automaticamente.

### Slide: Ferramenta: Juliet Test Suite (~45s)
**No TCC:** Seção 2.2.5.1 "Juliet Test Suite" (p. 42).
> "O *Juliet Test Suite* é uma coleção de programas escritos em C/C++ e Java, contendo casos de teste sintéticos, que foram desenvolvidas como exemplos de vulnerabilidades." (Seção 2.2.5.1, p. 42)
> "A versão mais recente 1.3 para C/C++ possui mais de 64 mil casos de teste espalhados em mais de 100 mil arquivos." (Seção 2.2.5.1, p. 42)
> "O propósito central é servir como um ``campo de provas'' padronizado para ferramentas de análise de código [...] Esse conjunto será utilizado para analisar todos os CWEs selecionados para este trabalho." (Seção 2.2.5.1, p. 42)

**Fala sugerida:**
- O Juliet Test Suite é uma coleção pública do NIST.
    - Possui milhares de casos de teste sintéticos em C, C++ e Java, cada um já rotulado com a CWE que representa.

- O ponto importante é que cada caso vem em par: uma versão vulnerável e uma versão corrigida do mesmo código.

- É a fonte de treino e teste da validação cruzada.

- Sendo também o piso de qualidade do Gate.
    - A regra só é aprovada se tiver zero falsos positivos nesse conjunto.

- Esse conjunto também foi utilizado para um dos modos de exemplo do gerador: o modo `pairs`.

---

## 3. Objetivos e método

### Slide: Objetivos e hipótese (~1 min)
**No TCC:** Seção 1.3 "Objetivos e hipótese" (p. 18-21): Subseção 1.3.1 "Objetivo geral" (p. 18), Subseção 1.3.2 "Objetivos específicos" (p. 19), Subseção 1.3.3 "Hipótese ou critério de validação" (p. 20).
> "O objetivo geral deste trabalho é demonstrar que um *framework* de síntese automatizada de regras [...] apresenta precisão e *recall* estatisticamente superiores às abordagens estáticas tradicionais [...] em, no mínimo, cinco categorias de [CWE]." (1.3.1, p. 18)
> "(1) Determinar os limites de detecção semântica [...]; (2) Avaliar o ganho quantitativo de desempenho [...]; (3) Determinar a viabilidade técnica [...] utilizando modelos de linguagem de menor escala." (1.3.2, p. 19)
> "A hipótese desta pesquisa é a de que a geração automatizada de regras [...] produzirá taxas de detecção [...] estatisticamente superiores [...] quando comparada aos conjuntos de regras predefinidos." (1.3.3, p. 20)

**Fala sugerida:**
- Nosso objetivo geral:
    - [Slide]

- Com nossos objetivos específicos como:
    - [Slide]

- A hipótese sendo que o modelo automatizado detecta vulnerabilidades com taxas estatisticamente superiores às abordagens tradicionais. 

### Slide: Arquitetura implementada (~1,5 min)
**No TCC:** Seção 3.2.3 "Arquitetura efetivamente implementada" (p. 55-56) e Seção 3.2.7 "Protocolo de avaliação" (p. 59).
> "O sistema implementado estrutura-se em dois papéis centrais executados por modelos de linguagem -- gerador e corretor -- e um componente determinístico, o *gate* de avaliação." (3.2.3, p. 55)
> "Uma regra é considerada **aprovada** quando [...] atinge *recall* mínimo de 50%, não produz nenhum falso positivo nos casos sintéticos do Juliet Test Suite e não ultrapassa 0,1 alertas por mil linhas de código (KLOC)." (3.2.3, p. 56)
> "A avaliação de cada regra sintetizada segue um protocolo de validação cruzada por dobras [...] com $k=5$ [...] cada configuração experimental foi repetida com múltiplas sementes [...] nas configurações consideradas mais relevantes, estendidas a cinco." (3.2.7, p. 59)
> "O teto de seis tentativas é um ajuste empírico, não o resultado de uma comparação dedicada entre diferentes valores de teto [...] Mesmo dentro desse novo orçamento, o mesmo comportamento de repetição persistiu em boa parte das execuções registradas -- em algumas configurações, o corretor reenviou a regra da tentativa anterior em até cinco das seis correções disponíveis." (3.2.3, p. 56, trecho adicionado nesta revisão)
> "em vez de reescrever a regra inteira a cada tentativa de correção, o corretor responde apenas com o novo valor de um único campo [...], escolhido ciclicamente a cada tentativa, enquanto o restante da regra permanece inalterado." (3.2.4 "Formatos de saída das regras", p. 57)

**Fala sugerida:**
- A arquitetura implementada é mais simplificada do que a antiga. 

- Com dois papéis de LLM e um componente determinístico no meio.

- O Gerador recebe exemplos de código vulnerável e seguro e escreve uma regra candidata.

- Essa regra passa pelo Gate, que é determinístico:
    - Ele valida a sintaxe, roda o SemGrep de verdade, e mede recall, precisão e falsos positivos.

- Se a regra é aprovada, ela vai para o conjunto final. 
- Se não, o Gate devolve o relatório de erro para o Corretor, que é outro papel de LLM, e ele gera uma nova versão — esse ciclo se repete até seis vezes.

- Esse teto de seis não veio de uma otimização formal.
    - Começamos com três — era o limite do desenho original — e vimos nas primeiras execuções o corretor travar, repetindo a mesma regra errada já na 3ª ou 4ª tentativa.
    - Mesmo dobrando, em boa parte das execuções, ele continuou repetindo a regra anterior em até 5 das 6 tentativas disponíveis. 
    - Foi exatamente esse travamento que levou criação no `field_correct`: em vez de pedir para o corretor reescrever a regra inteira de novo, ele corrige apenas o campo que o Gate apontou como errado.

- Temos um critério de aprovação é rigoroso de propósito:
    - Recall de pelo menos 50%, zero falsos positivos no Juliet Test Suite, e no máximo 0,1 alertas por mil linhas de código rodando sobre código real assumido como correto. 
    - E toda configuração relevante foi avaliada por validação cruzada, com até cinco sementes de particionamento diferentes.

- Semente é o número que define o sorteio de como o Juliet Test Suite é dividido nas 5 partes (folds) da validação cruzada.

- Trocar a semente refaz esse sorteio do zero; numa mesma semente, as 5 dobras só se revezam sendo teste, sem novo sorteio.

---

## 4. Resultados

*(Este é o bloco mais longo — é aqui que está a evidência do trabalho. Fale devagar, deixe os números "assentarem".)*

### Slide: Antes dos números: formato e combinação de modelo (~30s)
**No TCC:** Seção 3.2.4 "Formatos de saída das regras" (p. 57) + Seção 3.2.6 "Combinações de modelos avaliadas" (p. 58-59).
> "cinco formatos distintos de saída foram implementados e avaliados para a regra candidata, cada um restringindo de forma diferente a liberdade do modelo gerador." (3.2.4, p. 57)
> "a combinação D [...] demonstrou-se necessária para a obtenção dos melhores resultados [...]; a combinação C, baseada em um modelo de 4 bilhões de parâmetros, não foi capaz de reproduzir os ganhos obtidos pelo mecanismo `field_correct`." (3.2.6, p. 59)

**Fala sugerida:**
- Formato de saída é o quanto de liberdade eu dou para o modelo escrever a regra.
    - Indo de YAML livre até formsearch, que é todo travado por uma gramática formal.

- Combo é a combinação de modelo: qual LLM eu usei como gerador e corretor. 

### Slide: Nossas combinações de modelo (~40s)
**No TCC:** Seção 3.2.6 "Combinações de modelos avaliadas" (p. 58-59) + Tabela 3 "*Combinações de modelos de linguagem avaliadas*" (p. 58).
> "Todas as combinações utilizam o mesmo modelo de 3 bilhões de parâmetros (Qwen2.5-Coder-3B) na etapa de detecção inicial de vulnerabilidades, variando o modelo responsável pela geração e correção das regras." (3.2.6, p. 58)
> "A: Qwen2.5-Coder-3B em todos os papéis. B: Qwen2.5-Coder-7B. C: Qwen3-4B-Instruct-2507. D: Qwen3-Coder-30B-A3B (*Mixture-of-Experts*, aproximadamente 3 bilhões de parâmetros ativos por *token*). E: Qwen3-Coder-30B-A3B, sem troca de modelos entre papéis." (Tabela 3, p. 58 -- o TCC também avalia um combo F com Phi-4-mini, omitido no slide por não ser comentado na fala)
> "a combinação D [...] demonstrou-se necessária para a obtenção dos melhores resultados [...]; a combinação C [...] não foi capaz de reproduzir os ganhos obtidos pelo mecanismo `field_correct`, evidenciando uma relação direta entre a capacidade do modelo gerador e a eficácia de mecanismos de correção mais refinados." (3.2.6, p. 59)

**Fala sugerida:**
- Essa é a tabela completa das combinações.

- Todas usam o mesmo modelo pequeno, de 3 bilhões, para a detecção inicial; o que varia entre elas é só o modelo que gera e corrige a regra.

- Manter o modelo pequeno para a detecção inicial mantém o custo baixo para a análise total de projeto e apenas determina uma área de possíveis bugs.

- Diminuindo o trabalho para modelos mais pesados, atuando nos poucos achados encontrados.

- Vai de um modelo de 3 bilhões sozinho, no Combo A, até o Combo D.

- O Combo D tem 30 bilhões de parâmetros no total, mas é do tipo *Mixture-of-Experts*: a cada token, só uma fração pequena desses parâmetros entra em ação — cerca de 3 bilhões.

- Isso dá a capacidade de um modelo grande com o custo de processamento de um pequeno. O que ainda pesa é a memória então rodamos esse combo com *offload* parcial pra GPU.

- O Combo E é o mesmo modelo do D, mas sem trocar de modelo entre os papéis de gerador e corretor.

- O Combo D foi necessário para os melhores resultados — o Combo C, de 4 bilhões, não conseguiu aproveitar o mecanismo de correção mais refinado, o field_correct.

### Slide: Modo de exemplos: findings (padrão) (~30s)
**No TCC:** Seção 3.2.3 "Arquitetura efetivamente implementada" (p. 57) + Seção 3.2.5 "O analisador de grafos de eventos" (p. 58).
> "o parâmetro de modo de exemplos (`example_mode`), que determina o que é mostrado ao gerador -- os achados do detector (`findings`, padrão), pares de código vulnerável/seguro do *dataset* (`pairs`), achados da análise de grafos de eventos (`graph`) ou nenhum exemplo (`none`)." (3.2.3, p. 57)
> "testar se seus achados [...] constituiriam exemplos de treinamento de maior qualidade para o gerador do que os achados, predominantemente textuais, do detector inicial de 3 bilhões de parâmetros." (3.2.5, p. 58)

**Fala sugerida:**
- O modo de exemplos define o que eu mostro para o gerador antes de pedir a regra, tem quatro valores: findings, pairs, graph e none.

- findings é o padrão: o gerador recebe o relatório textual de um detector inicial, um modelo menor, de 3 bilhões de parâmetros, descrevendo em linguagem natural onde ele acha que está o defeito.

- Foi o modo usado nas primeiras rodadas, antes de eu testar qualquer alternativa.

- O problema é que essa descrição é só texto, não aponta as linhas exatas do código envolvidas.

### Slide: Modo de exemplos: pairs (~30s)
**No TCC:** Seção 3.3.3 "Revisão da configuração de referência e rodada final (CWE-416)" (p. 62).
> "a única configuração já aprovada pelo *gate* ao longo de todo o trabalho: a combinação D, formato `template`, com o parâmetro `example_mode=pairs` (pares de código vulnerável e seguro apresentados ao gerador, em vez dos achados do detector), aplicada ao CWE-416." (Seção 3.3.3, p. 62)

**Fala sugerida:**
- Em pairs, o gerador recebe, lado a lado, o próprio par de código do Juliet: a versão vulnerável e a versão corrigida do mesmo trecho.

- É o parâmetro da única configuração que conseguimos aprovar pelo Gate em todo o trabalho.

- A vantagem sobre o findings é mostrar para o modelo não só onde está o defeito, mas o que diferencia o código com bug do código seguro.

### Slide: Modo de exemplos: graph (~45s)
**No TCC:** Seção 3.2.5 "O analisador de grafos de eventos" (p. 57-58) + Seção 3.4.5 "O que não foi alcançado", item (v) (p. 69) + Tabela "*Efeito de* `example_mode=graph`" (p. 69).
> "o modo de exemplos `graph` [...] é alimentado por um componente [...] que não utiliza nenhum modelo de linguagem: um analisador de grafos de eventos de memória." (3.2.5, p. 57)
> "Substituir os achados do detector inicial pelos achados do analisador de grafos como exemplo de treinamento (`example_mode=graph`) elevou o *recall* da combinação D no CWE-416 de 71,6% para 91,6%, porém às custas de uma queda de precisão de 89,4% para 69,8% [...]: a regra tornou-se mais abrangente, não mais silenciosa." (3.4.5, item v, p. 69)
> "a descrição de um achado do grafo [...] informa ao modelo onde está o defeito, mas não o que a regra deve excluir." (3.4.5, item v, p. 69)

**Fala sugerida:**
- graph vem de um componente à parte que construímos, sem nenhum LLM: o analisador de grafos de eventos de memória, que aponta as duas linhas exatas do defeito — a liberação e o uso.

- Troquei os achados do detector pelos achados do grafo como exemplo, no CWE-416, use after free, e o recall subiu de 71,6% para 91,6%.

- Só que o preço foi alto: a precisão caiu de 89,4% para 69,8%, e os falsos positivos no Juliet foram de 9 para quase 30.

- A causa: o achado do grafo diz onde está o problema, mas não ensina o modelo a excluir a própria linha de liberação do padrão de uso perigoso.

- Identificando o limite da linguagem YAML para criar uma regra complexa o suficiente de identificar devidamente.

### Slide: Mecanismos do corretor: guard e project_apis (~30s)
**No TCC:** Seção 3.2.3 "Arquitetura efetivamente implementada" (p. 57).
> "o *guard*, que impede que uma correção substitua a melhor regra já encontrada caso a nova versão apresente pontuação inferior; o `project_apis`, que insere no *prompt* os nomes das funções de memória próprias do projeto-alvo." (3.2.3, p. 57)

**Fala sugerida:**
- Dois mecanismos do corretor, fora do modo de exemplos: guard nunca deixa ele trocar a melhor regra já encontrada por uma pior.

- project_apis insere no prompt os nomes de função de memória do próprio projeto que está sendo analisado.

- Juntos, eles elevaram o recall do CWE-416 — mas à custa de um salto de ruído.

### Slide: Síntese dos resultados por CWE (~1,5 min)
**No TCC:** Seção 3.4 "Resultados e análises", abertura (p. 62) + Tabela 4 "*Síntese dos melhores resultados por CWE*" (p. 62).
> "A Tabela [4] sintetiza o melhor resultado obtido para cada categoria de vulnerabilidade avaliada ao longo do trabalho." (3.4, p. 62)

**Fala sugerida:**
- Melhor resultado obtido em cada uma das cinco categorias.

- Olhando rápido: o CWE-416, uso após liberação, foi o único que teve dobras efetivamente aprovadas pelo Gate.
    - Só em duas das cinco sementes. 

- O CWE-415, double free, chegou perto, com recall relevante, mas nunca foi aprovado. 

- E as outras três — 401, 476 e 457 — ficaram com desempenho insuficiente.

### Slide: CWE-416: evolução até a melhor configuração (~1,5 min)
**No TCC:** Seção 3.4.3 "CWE-416: da aprovação isolada à melhoria consistente" (p. 63-65) + Tabela 5 "*Evolução da configuração de referência para o CWE-416*" (p. 64) + Figura 12 (placeholder, p. 64) + item (iii) da Seção 3.4.5 "O que não foi alcançado" (p. 67), que relata a combinação `pairs+guard+project_apis`.
> "A combinação do parâmetro `pairs` com os mecanismos `guard` e `project_apis` elevou ainda mais o *recall* [...] porém às custas de um aumento severo de ruído (619 a 799 falsos positivos [...])." (3.4.3, p. 64)
> "Isolando apenas o mecanismo `guard` (sem o `project_apis`) [...] obteve-se o melhor resultado do trabalho [...] com uma faixa de *recall* mais concentrada (89,2% a 100%)." (3.4.3, p. 64-65)
> "O resultado mostrou o oposto: a taxa de falsos positivos aumentou em uma ordem de grandeza [...] o isolamento posterior do `project_apis` como variável causadora só foi possível por meio de uma rodada adicional." (3.4.5, item iii, p. 67)

**Fala sugerida:**
- Começamos com a configuração `pairs`, que já superava a regra tradicional, mas ainda tinha de 84 a 320 falsos positivos.

- Somando dois mecanismos que pareciam bons isoladamente — `guard` e `project_apis`, que injeta no prompt os nomes de função do próprio projeto.
    - O resultado foi o oposto do esperado: os falsos positivos dispararam para a faixa de 619 a 799.

- Isolamos as variáveis numa rodada extra e descobrimos que o `project_apis` que aumentava, quanto mais informação pode ajudar ou confundir, e esse foi o caso. 
    - Removendo ele e mantendo só o `guard`, chegamos à melhor configuração do trabalho inteiro: recall de 89,2% a 100%, com falsos positivos entre 12 e 216 — e duas das cinco sementes efetivamente aprovadas pelo Gate.
*(Se já tiver o gráfico no lugar do placeholder: 'o gráfico mostra bem esse salto e a queda depois'.)*"

### Slide: CWE-415: a lição metodológica das sementes (~1,5 min)
**No TCC:** Seção 3.4.4 "CWE-415 e a necessidade metodológica de múltiplas sementes" (p. 65-66) + Tabela 6 "*Recall por semente de particionamento [...] CWE-415*" (p. 65) + Figura 13 (placeholder, p. 66).
> "suas duas sementes originais apresentaram *recall* de 63,8% e 64,8% [...] que, isoladamente, sugeririam um resultado estável em torno de 64%. A extensão para cinco sementes revelou uma realidade distinta: 63,8%, 64,8%, 47,3%, 43,3% e 76,3%, uma amplitude de 33 pontos percentuais." (3.4.4, p. 65)
> "a variação de resultado entre sementes de particionamento foi, em diversos casos, maior do que o efeito de qualquer mecanismo experimental avaliado." (3.4.4, p. 66)

**No slide:** tabela com as 5 sementes e seus recalls; 3 bullets (amplitude de 33 p.p.; nunca aprovada pelo gate; lição metodológica); aviso de gráfico pendente.

**Fala sugerida:**
- Na configuração de referência do CWE-415, as duas primeiras sementes que testei deram recall de 63,8% e 64,8% — valores bem próximos, que sugeririam um resultado estável.
    - Quando estendi para cinco sementes, apareceram também 47,3%, 43,3% e 76,3%. 
    - Sendo muito instável.

- Quase foi passado despercebido sua instabilidade.
    - A regra nunca foi aprovada pelo Gate — porque recall alto e baixo ruído em código real nunca aconteceram juntos, na mesma semente.

### Slide: A regra sintetizada supera a regra tradicional (~2 min — slide mais importante)
**No TCC:** Seção 3.4.6 "Comparação com um analisador estático tradicional" (p. 71-73) + Tabela 9 "*Comparação entre as regras sintetizadas e um analisador tradicional*" (p. 72) + Figura 14 (placeholder, p. 72).
> "O registro público [...] do SemGrep [...] disponibiliza o pacote `r/c` [...] duas regras mostraram-se diretamente relevantes [...]: `c.lang.security.function-use-after-free`, para o CWE-416, e `c.lang.security.double-free` [...] para o CWE-415." (3.4.6, p. 71)
> "a melhor configuração sintetizada por este trabalho superou a regra tradicional em *recall* em todas as cinco sementes avaliadas, sem exceção." (3.4.6, p. 72)
> "a precisão [...] apresenta um quadro mais equilibrado [...] evidenciando que o ganho de *recall* [...] não ocorre sem nenhum custo de precisão, ainda que o ganho líquido, medido pelo F1-Score, seja favorável em todas as sementes avaliadas." (3.4.6, p. 73)

**Fala sugerida:**
- De todos os experimentos, apenas duas CWEs passaram do gate.

- Temos duas regras relevantes do registro público e gratuito do SemGrep para esses CWEs.

- Para o CWE-416, a regra tradicional tem recall de 17,4%, deixando passar cerca de cinco em cada seis casos reais de uso após liberação.
- Com a nossa melhor configuração chega de 89,2% a 100%.

- Para o CWE-415, a tradicional tem 28,7% de recall;
- A sintetizada vai de 43,3% a 76,3%.

- Essa superioridade em recall e em F1-Score acontece em todas as cinco sementes avaliadas, nos dois CWEs, sem nenhuma exceção. 

- A precisão tem um quadro mais equilibrado, em algumas sementes a regra tradicional é mais precisa, mas o ganho, medido pelo F1, é sempre favorável à regra sintetizada.
*(Pausa curta aqui. É o número que a banca vai lembrar.)*"

### Slide: O que não funcionou — um limite da linguagem, não da busca (~1,5 min)
**No TCC:** Seção 3.4.1 "CWE-457: um alvo estruturalmente inadequado" (p. 62-63, para o ponto do CWE-457) + Seção 3.4.5 "O que não foi alcançado", item (vi) (p. 68-69, para o diagnóstico CWE-401/415/476) + Tabela 7 (p. 68) e Tabela 8 (p. 70), que sustentam os experimentos finais citados no item (vi).
> "o teto de *recall* de aproximadamente 31% obtido manualmente [...] já está abaixo do limiar mínimo de 50% exigido pelo *gate*." (3.4.1, p. 63)
> "**CWE-401** [...] é um argumento de vivacidade (*liveness*) sobre todos os caminhos até todas as saídas da função, não uma relação entre dois pontos fixos de código [...] que uma regra de *taint* possa nomear." (3.4.5, item vi, p. 68)
> "**CWE-415** [...] a fonte e o sumidouro de contaminação são [...] exatamente o mesmo padrão sintático (`free($P)`); o motor de *taint* do SemGrep casa essa única ocorrência contra si mesma." (3.4.5, item vi, p. 68-69)
> "**CWE-476** [...] a ausência de um teste não nulo em qualquer caminho [...] é uma condição sobre caminhos de fluxo de controle, não uma forma sintática única que possa ser nomeada e excluída de uma vez." (3.4.5, item vi, p. 69)
> "O fato de essas três causas se manterem idênticas através de métodos tão distintos quanto um modelo de 30 bilhões de parâmetros [...] um gerador determinístico por síntese de padrões e um programa que compila a lógica do grafo diretamente em uma regra fixa [...] é [...] a evidência mais forte [...] de que o limite não está na busca, mas no destino dela." (3.4.5, item vi, p. 69)

**No slide:** 4 bullets (um por CWE sem solução: 457, 401, 415, 476) + 1 linha de fechamento sobre os três métodos de confirmação.

**Fala sugerida:**
- As outras três categorias não funcionaram, e investigando a fundo o porquê:
    - A causa é a mesma nos três casos: um limite da linguagem de padrões do SemGrep.

- No CWE-457, o motor do SemGrep sequer inicia o rastreamento de contaminação a partir de uma declaração sem valor atribuído.
    - Tendo um teto de recall conhecido de cerca de 31%, abaixo do piso que exigimos.

- No CWE-401, o vazamento de memória: uma regra de taint só sabe perguntar "esse valor, de um ponto fixo A, chega a um outro ponto fixo B?" — uma relação entre dois lugares nomeados no código.
    - Vazamento não é isso. É a ausência de um `free` em pelo menos um dos caminhos possíveis entre a alocação e toda saída da função, não dá pra apontar dois pontos fixos, tenho que olhar todo caminho até toda saída.
    - Essa vivacidade é algo muito mais rico do que o que uma regra de taint consegue expressar.

- No CWE-415, é o mesmo padrão sintático — `free` de uma variável, e o motor de taint do SemGrep não é capaz de acompanhar.

- E no CWE-476, cai no mesmo caminho.
    - A ausência de um teste de nulo em qualquer caminho é uma condição sobre caminhos de execução, não uma forma sintática única que dê para excluir de uma vez.

- O que torna essa conclusão forte é nossa confirmação por três métodos completamente diferentes.
    - A primeira é o modelo de 30 bilhões, orientado pelos achados do grafo — usa LLM e passa pelo ciclo gerador-corretor normal, com busca.
    - A segunda é o gerador determinístico, o `method_synthesis` — sem LLM nenhum. Ele testa combinações de padrões de código tiradas dos próprios achados do grafo, e vai guardando só o que cobre mais casos sem dar falso positivo. É busca por tentativa e erro, não rede neural.
    - A terceira é uma regra compilada direto da lógica do grafo — sem LLM e sem busca nenhuma, só traduzo mecanicamente o que o analisador de grafos já sabe pra sintaxe do SemGrep.

- Por que isso descarta o modelo e o método?
    - Se o problema fosse do modelo, as abordagens 2 e 3, que não usam LLM, deveriam escapar.
    - Se o problema fosse do método de busca, a abordagem 3, que não faz busca nenhuma, deveria escapar.

- Nenhuma escapou. As três erram pela mesma causa, específica de cada CWE. 

- A única coisa que elas têm em comum é que todas precisam terminar numa regra SemGrep — e é aí, na linguagem de padrões em si, que mora o limite, não na busca que leva até ela.

---

## 5. Conclusão

### Slide: Conclusão (~1,5 min)
**No TCC:** Seção 4.1 "Retomada do problema e dos objetivos" (p. 74) + Seção 4.2 "Contribuições para a Computação" (p. 75) + Seção 4.3 "Limitações e trabalhos futuros" (p. 76).
> "A resposta obtida é condicional, não categórica: sim, para duas das cinco categorias de CWE [...] (CWE-416 e CWE-415) [...]; não demonstrada, para as demais três." (4.1, p. 74)
> "Dos três Objetivos Específicos [...] o primeiro [...] e o terceiro [...] foram plenamente alcançados; o segundo [...] foi parcialmente alcançado." (4.1, p. 74)
> "Contribui-se ainda com um diagnóstico que distingue [...] um limite de **busca** de um limite de **linguagem-alvo**." (4.2, p. 75)
> "uma regra pode satisfazer integralmente um critério de aprovação quantitativo [...] sem que seus alertas individuais correspondam a defeitos verdadeiros quando lidos manualmente [...] o que reforça [...] a necessidade de revisão manual amostral." (4.2, p. 75)
> "propõe-se: (i) validar as configurações já aprovadas sobre múltiplos repositórios de negativos do mundo real [...]; [...] (vi) [...] investigar um motor de análise estática com sensibilidade a caminho [...] (como o CodeQL ou o Joern)." (4.3, p. 76)

**No slide:** 5 bullets — hipótese parcialmente confirmada; objetivos 1/3 plenos, 2 parcial; contribuição central (busca × linguagem-alvo); achado complementar (gate ≠ verdade); próximos passos.

**Fala sugerida:**
- Voltando à hipótese: 
    - Ela não se confirma na forma ampla, para as cinco categorias. 
    - Mas nas duas categorias em que conseguimos uma regra tradicional para comparar, a hipótese não é refutada: o ganho é real.

- Dos três objetivos específicos, o primeiro e o terceiro foram plenamente alcançados; 
- O segundo, parcialmente — porque só pude comparar quantitativamente com a linha de base tradicional em dois CWEs.

- A contribuição deste trabalho é a distinção entre um limite de busca e um limite da linguagem-alvo. 
    - Isso é algo que qualquer pessoa tentando sintetizar regras para o SemGrep — ou para qualquer outra ferramenta baseada em padrões — pode usar antes de gastar tempo testando variações de prompt ou de modelo.

- Um achado também é que a aprovação pelo Gate não é garantia de que os alertas são verdadeiros em código real, e reforça que revisão manual continua sendo necessária.

- Como próximos passos, os dois mais concretos são: 
    - Em todo o trabalho, código real já entrou na avaliação — o git/git foi o gate de negativos em toda rodada, é ele que decide se uma regra passa ou não no critério de ruído. Só que é um projeto só. Então o próximo passo não é "testar em código real pela primeira vez", é confirmar que essa taxa baixa de falso positivo se mantém em outros repositórios, e não é uma peculiaridade do git/git.
    - E explorar motores com sensibilidade a caminho, como CodeQL ou Joern, para os três CWEs que a linguagem do SemGrep não consegue expressar.

- Obrigado.

### Slide: Obrigado! (~10s)
**No TCC:** não se aplica (slide de encerramento).
*(Sem fala adicional — pausa, sorriso, espera a primeira pergunta da banca.)*

---

## Apêndice — só usar se a banca perguntar (sem tempo fixo)

Estes quatro slides não entram nos 15 minutos. Use-os como referência rápida para responder; não precisa decorar um discurso, só saber onde cada número está.

### Trabalhos correlatos
**No TCC:** Seção 2.3 "Trabalhos correlatos" (p. 44-52): 2.3.1 KNighter (p. 45-46), 2.3.2 Hou et al. (p. 47-48), 2.3.3 RepoAudit (p. 49-51), 2.3.4 "Síntese comparativa" + Tabela 2 (p. 51-52).
> "KNighter relata dentre 37 *checkers* plausíveis, foram relatados 92 novos *bugs*, que depois de uma inspeção manual, 32,2% foram falsos positivos." (2.3.1, p. 46)
> "Resultados de Hou et al. criaram 41 regras válidas comparadas com as 37 geradas por Yang et al." (2.3.2, p. 48)
> "O agente [RepoAudit] [...] totalizando 40 verdadeiros positivos e 11 falsos positivos, uma precisão de 78,43%." (2.3.3, p. 50)

**Fala sugerida:**
"Se a banca perguntar como isso se compara com a literatura: o KNighter foi pioneiro, gerando checkers para o Clang a partir de commits, mas tinha 32% de falsos positivos nos novos achados. O Hou et al. também sintetiza regras SemGrep e superou o KNighter em número de regras válidas. O RepoAudit é o mais sofisticado — um agente com memória — mas ele reconsulta o LLM a cada auditoria, o que tem custo recorrente. A diferença central do meu trabalho é que o LLM só atua na geração da regra; a execução final no SemGrep não tem custo de inferência nenhum."

### O analisador de grafos de eventos
**No TCC:** Seção 3.2.5 "O analisador de grafos de eventos: um componente complementar e determinístico" (p. 57-58).
> "o analisador atingiu 134 dos 138 casos de CWE-416 do Juliet Test Suite, sem nenhum falso positivo, e manteve-se abaixo do limite de 0,1 alertas por KLOC [...] (entre eles *tmux*, *PostgreSQL* e *SQLite*), embora tenha falhado em outros (no *vim*, uma única função de liberação inferida incorretamente respondeu por 179 dos 234 alertas emitidos)." (3.2.5, p. 58)

**Fala sugerida:**
"Esse é um componente que construí à parte, sem nenhum LLM, só para testar se uma abordagem totalmente determinística chegaria ao mesmo critério de qualidade. Ele constrói um grafo de eventos de memória por função e faz busca de alcançabilidade. Sozinho, ele acertou 134 dos 138 casos de CWE-416 do Juliet, sem nenhum falso positivo, e passou no critério de ruído real em projetos como tmux, PostgreSQL e SQLite — mas falhou no vim, porque inferiu errado uma função de liberação. Também usei os achados dele como exemplo para o gerador, mas isso é outra história, está no texto."

### Formatos de regra e combinações de modelo
**No TCC:** Seção 3.2.4 "Formatos de saída das regras" (p. 57) + Seção 3.2.6 "Combinações de modelos avaliadas" (p. 58-59) + Tabela 3 (p. 59) + Seção 3.4.2 "Mecanismo `field_correct`: um ganho real, porém inconsistente" (p. 63), para o detalhe do `field_correct`.
> "cinco formatos distintos de saída foram implementados [...]: `yaml` [...] `spec` [...] `template` [...] `form` [...] `formsearch`." (3.2.4, p. 57)
> "a combinação D [...] demonstrou-se necessária para a obtenção dos melhores resultados [...]; a combinação C, baseada em um modelo de 4 bilhões de parâmetros, não foi capaz de reproduzir os ganhos obtidos pelo mecanismo `field_correct`." (3.2.6, p. 59)

**Fala sugerida:**
"Testei cinco formatos de saída, do mais livre (YAML puro) ao mais restrito (formsearch, com gramática formal). E testei seis combinações de modelo, de 3 bilhões a 30 bilhões de parâmetros. O ponto principal: um modelo de 4 bilhões roda localmente e funciona, mas só o modelo de 30 bilhões conseguiu aproveitar o mecanismo de correção mais refinado, o field_correct."

### Contribuições (Design Science Research)
**No TCC:** Seção 4.2 "Contribuições para a Computação" (p. 75), itens (1)-(4).
> "(1) **Constructo**: a caracterização [...] dos cinco formatos de saída de regra [...]. (2) **Método**: o mecanismo de correção por campo [...]. (3) **Modelo**: a demonstração empírica [...] de que a variação amostral entre sementes pode exceder o efeito de qualquer mecanismo experimental avaliado. (4) **Instanciação**: o *pipeline* completo e executável." (4.2, p. 75)

**Fala sugerida:**
"Organizei as contribuições nos quatro tipos de artefato do DSR: um constructo (a caracterização dos cinco formatos de regra), um método (a caracterização do field_correct como ganho condicional), um modelo (a evidência de que a variação entre sementes pode superar qualquer efeito experimental) e uma instanciação (o pipeline completo, que roda em hardware de consumo)."

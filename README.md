# Nível 1 da Carreira de Governança de Dados Alura

## Descrição do projeto
Discutir no fórum
A equipe de Governança de Dados do SwiftBank te integrou em um projeto de fundação. A organização cresceu rapidamente nos últimos dois anos e hoje convive com problemas clássicos:
 áreas com definições divergentes de "cliente ativo", 
 planilhas paralelas, 
 retrabalho entre Marketing, 
 Crédito e Financeiro, dúvidas recorrentes sobre quem aprova o uso de dados pessoais e relatórios regulatórios feitos sob pressão. A diretoria patrocinou a criação de um programa de governança e te convidou para entregar os artefatos fundacionais do Nível 1: um mapa de papéis, o ciclo de vida dos dados aplicado a um caso real, uma política escrita com indicadores e um glossário/catálogo inicial com metadados.

O projeto é majoritariamente documental e diagramático, condizente com o perfil de Governança de Dados. Apenas uma etapa utiliza um pequeno script em Python para gerar uma análise simples de qualidade de metadados. Os entregáveis devem ser organizados em uma pasta no no seu computador chamada governanca-swiftbank-nivel1/, contendo subpastas por etapa e um README curto em Excel ou documento explicando o que está em cada arquivo.

A pessoa que conduz o projeto deve atuar como analista de governança: traduzir necessidades de negócio em artefatos compreensíveis, padronizar definições, mapear responsabilidades e propor mecanismos de medição.

# Preparando o ambiente

Discutir no fórum
Draw.io (versão web em app.diagrams.net) para diagramas e organogramas.
Excel para planilhas de glossário, política, métricas e dicionário de dados.
ChatGPT (ou outro LLM) para apoio na redação de definições e revisão de textos.
Google Colab com Python e Pandas para a etapa única de análise de qualidade de metadados (4ª etapa).
Pasta de trabalho governanca-swiftbank-nivel1/, com subpastas: 01_organograma/, 02_ciclo_de_vida/, 03_politica/, 04_glossario_metadados/.
Como o domínio envolve dados, são fornecidos abaixo dois datasets fictícios que servirão de insumo para o glossário, dicionário de dados e análise de qualidade de metadados. Os campos foram criados especificamente para esse exercício.

clientes_swiftbank.csv — Cadastro fictício de clientes do banco digital
Dicionário de dados resumido:

id_cliente: identificador único do cliente (string).
nome_completo: nome fictício (string).
data_nascimento: data de nascimento no formato AAAA-MM-DD.
tipo_pessoa: PF ou PJ.
segmento: Varejo, Premium, Empresarial.
data_abertura_conta: data de abertura da conta.
status_conta: Ativa, Inativa, Encerrada.
produto_principal: Conta Corrente, Cartão, Empréstimo, Investimento.
cidade: cidade fictícia.
consentimento_marketing: Sim/Não (LGPD).

Copiar
id_cliente,nome_completo,data_nascimento,tipo_pessoa,segmento,data_abertura_conta,status_conta,produto_principal,cidade,consentimento_marketing
CLI001,Ana Ribeiro,1990-04-12,PF,Varejo,2021-03-15,Ativa,Conta Corrente,Recife,Sim
CLI002,Bruno Salles,1985-11-02,PF,Premium,2019-06-20,Ativa,Investimento,São Paulo,Sim
CLI003,Carla Tavares,1978-02-25,PF,Varejo,2020-01-10,Inativa,Cartão,Curitiba,Não
CLI004,Diego Monteiro,1995-09-30,PF,Varejo,2022-07-05,Ativa,Empréstimo,Belo Horizonte,Sim
CLI005,Elis Prado,1988-12-19,PF,Premium,2018-04-22,Ativa,Conta Corrente,Porto Alegre,Sim
CLI006,Felipe Borges,2000-05-08,PF,Varejo,2023-01-18,Ativa,Cartão,Salvador,Não
CLI007,Construtora Norte LTDA,2010-08-14,PJ,Empresarial,2017-09-12,Ativa,Conta Corrente,Manaus,Sim
CLI008,Helena Costa,1992-07-22,PF,Varejo,2021-11-30,Encerrada,Conta Corrente,Fortaleza,Não
CLI009,Igor Almeida,1983-03-04,PF,Premium,2016-02-09,Ativa,Investimento,Rio de Janeiro,Sim
CLI010,Joana Vieira,1997-10-16,PF,Varejo,2022-05-25,Ativa,Cartão,Goiânia,Sim
CLI011,Kléber Rocha,1975-06-29,PF,Varejo,2019-12-01,Inativa,Empréstimo,Vitória,Não
CLI012,Larissa Souza,2001-01-11,PF,Varejo,2023-08-08,Ativa,Cartão,Florianópolis,Sim
CLI013,Marcos Dias,1986-04-05,PF,Premium,2015-10-19,Ativa,Investimento,Brasília,Sim
CLI014,Tech Sul Comercio,2015-03-21,PJ,Empresarial,2020-06-30,Ativa,Empréstimo,Curitiba,Sim
CLI015,Olivia Campos,1993-08-17,PF,Varejo,2021-02-14,Ativa,Conta Corrente,Natal,Não
CLI016,Paulo Henrique Lima,1980-11-26,PF,Varejo,2018-08-03,Encerrada,Cartão,Maceió,Não
CLI017,Quésia Martins,1996-02-07,PF,Varejo,2022-12-12,Ativa,Cartão,Aracaju,Sim
CLI018,Rafael Andrade,1989-09-09,PF,Premium,2017-04-27,Ativa,Investimento,São Luís,Sim
CLI019,Sabrina Queiroz,1998-06-15,PF,Varejo,2023-03-03,Ativa,Conta Corrente,Teresina,Não
CLI020,Agroindustrial Verde SA,2008-05-19,PJ,Empresarial,2014-11-05,Ativa,Investimento,Cuiabá,Sim
CLI021,Tiago Ferreira,1991-01-23,PF,Varejo,2020-09-09,Inativa,Cartão,Belém,Não
CLI022,Ursula Neves,1984-07-30,PF,Premium,2016-07-18,Ativa,Investimento,Campo Grande,Sim
CLI023,Vinícius Paiva,1999-12-04,PF,Varejo,2023-10-21,Ativa,Empréstimo,João Pessoa,Sim
CLI024,Wanda Pacheco,1977-03-08,PF,Varejo,2019-05-16,Ativa,Conta Corrente,Palmas,Não
CLI025,Xavier Lopes,1994-10-13,PF,Varejo,2021-07-07,Encerrada,Cartão,Boa Vista,Não
CLI026,Yara Cunha,2002-04-29,PF,Varejo,2023-11-15,Ativa,Conta Corrente,Macapá,Sim
CLI027,Zé Roberto Pinto,1973-08-21,PF,Varejo,2017-03-22,Ativa,Empréstimo,Rio Branco,Sim
CLI028,Loja Bom Café ME,2018-09-12,PJ,Empresarial,2021-04-04,Ativa,Conta Corrente,Porto Velho,Sim
CLI029,Beatriz Moura,1987-05-06,PF,Premium,2015-11-11,Ativa,Investimento,São Paulo,Sim
CLI030,Camila Sá,1992-02-18,PF,Varejo,2020-10-28,Ativa,Cartão,Recife,Não
CLI031,Daniel Tavares,1995-07-14,PF,Varejo,2022-02-02,Ativa,Cartão,São Paulo,Sim
CLI032,Editora Letra Viva,2012-12-01,PJ,Empresarial,2019-03-10,Inativa,Conta Corrente,Curitiba,Não
CLI033,Fátima Lopes,1981-10-25,PF,Varejo,2018-01-31,Ativa,Empréstimo,Salvador,Sim
CLI034,Gustavo Reis,1990-03-11,PF,Premium,2016-05-25,Ativa,Investimento,Belo Horizonte,Sim
CLI035,Heloísa Pires,1998-08-08,PF,Varejo,2023-06-17,Ativa,Conta Corrente,Fortaleza,Não
CLI036,Ícaro Mendes,1986-06-21,PF,Varejo,2020-04-13,Ativa,Cartão,Recife,Sim
CLI037,Janaína Rolim,1993-11-29,PF,Varejo,2021-12-20,Encerrada,Cartão,Natal,Não
CLI038,Construir Mais EIRELI,2016-07-07,PJ,Empresarial,2022-08-08,Ativa,Empréstimo,Vitória,Sim
CLI039,Lúcia Falcão,1979-04-04,PF,Premium,2014-10-02,Ativa,Investimento,Rio de Janeiro,Sim
CLI040,Murilo Antunes,2000-12-12,PF,Varejo,2023-09-25,Ativa,Cartão,Florianópolis,Sim
CLI041,Natália Bastos,1991-05-19,PF,Varejo,2020-03-30,Inativa,Conta Corrente,Goiânia,Não
CLI042,Otávio Camelo,1984-09-23,PF,Varejo,2017-12-15,Ativa,Empréstimo,Brasília,Sim
CLI043,Patrícia Mello,1996-01-31,PF,Varejo,2022-06-06,Ativa,Cartão,Manaus,Não
CLI044,Quirino Sobrinho,1972-02-14,PF,Varejo,2015-08-19,Ativa,Conta Corrente,São Paulo,Sim
CLI045,Renata Moreira,1989-07-27,PF,Premium,2018-11-09,Ativa,Investimento,Curitiba,Sim

metadados_tabelas_swiftbank.csv — Catálogo inicial (incompleto) de metadados
Dicionário de dados resumido:

tabela: nome físico da tabela.
camada: bronze, silver ou gold (algumas linhas estão erradas).
coluna: nome da coluna.
descricao: descrição da coluna (algumas vazias ou genéricas).
tipo_dado: tipo (string, int, date, decimal).
confidencialidade: aberto, restrito, confidencial (algumas vazias).
dado_pessoal: Sim/Não (algumas vazias).
responsavel: nome do owner/steward (algumas vazias).

Copiar
tabela,camada,coluna,descricao,tipo_dado,confidencialidade,dado_pessoal,responsavel
bz_clientes,bronze,id_cliente,Identificador único do cliente,string,restrito,Não,Marina Souza
bz_clientes,bronze,nome_completo,Nome completo do cliente,string,confidencial,Sim,Marina Souza
bz_clientes,bronze,cpf,,string,confidencial,Sim,
bz_clientes,bronze,data_nascimento,Data,date,confidencial,Sim,Marina Souza
bz_clientes,bronze,email,E-mail informado pelo cliente no cadastro,string,confidencial,Sim,Marina Souza
sl_clientes,silver,id_cliente,Identificador único do cliente após harmonização,string,restrito,Não,Marina Souza
sl_clientes,silver,nome_completo,Nome do cliente,string,confidencial,Sim,Marina Souza
sl_clientes,silver,idade,Idade calculada a partir da data de nascimento na data de referência,int,restrito,Sim,Marina Souza
sl_clientes,silver,segmento,,string,,,
sl_clientes,silver,cidade,Cidade,string,restrito,Não,Marina Souza
gd_clientes_ativos,gold,id_cliente,Identificador único do cliente,string,restrito,Não,Marina Souza
gd_clientes_ativos,gold,segmento,Segmento comercial do cliente (Varejo, Premium, Empresarial),string,restrito,Não,Marina Souza
gd_clientes_ativos,gold,flag_ativo,Indicador se cliente é considerado ativo segundo a regra do glossário,int,restrito,Não,Marina Souza
gd_clientes_ativos,gold,data_referencia,Data,date,aberto,Não,
bz_transacoes,bronze,id_transacao,ID da transação,string,restrito,Não,Lucas Andrade
bz_transacoes,bronze,id_cliente,ID do cliente que originou a transação,string,restrito,Não,Lucas Andrade
bz_transacoes,bronze,valor,Valor monetário da transação em reais,decimal,confidencial,Não,Lucas Andrade
bz_transacoes,bronze,data,,date,,,Lucas Andrade
bz_transacoes,bronze,tipo,Tipo,string,restrito,Não,Lucas Andrade
sl_transacoes,silver,id_transacao,Identificador da transação harmonizado,string,restrito,Não,Lucas Andrade
sl_transacoes,silver,id_cliente,Identificador do cliente,string,restrito,Não,Lucas Andrade
sl_transacoes,silver,valor_brl,Valor da transação em reais convertido a partir da moeda original,decimal,confidencial,Não,Lucas Andrade
sl_transacoes,silver,data_efetivacao,Data em que a transação foi efetivada e liquidada na conta,date,restrito,Não,Lucas Andrade
sl_transacoes,silver,categoria,Categoria,string,,Não,
gd_metricas_credito,gold,id_cliente,Identificador único do cliente,string,restrito,Não,Patrícia Lemos
gd_metricas_credito,gold,score_credito,Score de crédito calculado pelo modelo interno na data de referência,int,confidencial,Sim,Patrícia Lemos
gd_metricas_credito,gold,faixa_score,Faixa do score (baixo, médio, alto),string,restrito,Sim,Patrícia Lemos
gd_metricas_credito,gold,data_referencia,Data,date,aberto,Não,Patrícia Lemos
gd_metricas_credito,dashboard,modelo_versao,Versão do modelo de score utilizado na execução,string,restrito,Não,
bz_emprestimos,bronze,id_emprestimo,ID,string,restrito,Não,Roberto Vaz
bz_emprestimos,bronze,id_cliente,ID do cliente,string,restrito,Sim,Roberto Vaz
bz_emprestimos,bronze,valor_solicitado,Valor solicitado pelo cliente no momento da contratação do empréstimo,decimal,confidencial,Não,Roberto Vaz
bz_emprestimos,bronze,prazo_meses,Prazo,int,,Não,
sl_emprestimos,silver,id_emprestimo,Identificador único do empréstimo,string,restrito,Não,Roberto Vaz
sl_emprestimos,silver,id_cliente,Identificador do cliente tomador,string,restrito,Sim,Roberto Vaz
sl_emprestimos,silver,valor_aprovado,Valor efetivamente aprovado após análise de crédito,decimal,confidencial,Não,Roberto Vaz
sl_emprestimos,silver,taxa_juros,Taxa de juros mensal aplicada ao contrato,decimal,restrito,Não,Roberto Vaz
sl_emprestimos,silver,status,,string,,,

# 1ª Etapa: Mapa de papéis e organograma de governança do SwiftBank

Discutir no fórum
A primeira tarefa é entender quem é quem na governança de dados do banco. A diretoria pediu um organograma claro, em três camadas (estratégica, tática e operacional), com os papéis nomeados, suas responsabilidades resumidas e a relação entre eles. O entregável servirá como referência institucional e será apresentado em comitê.

Pergunta-chave: "Em uma estrutura como o SwiftBank, quem decide, quem traduz, quem operacionaliza e quem usa os dados, e como essas pessoas se conectam?"

Sua missão:

No Draw.io, monte um organograma em três camadas para o SwiftBank: estratégica (CDO, Comitê/DGO de Governança, Board patrocinador e DPO), tática (Data Owners das áreas Comercial, Crédito, Financeiro, Marketing, Operações e Jurídico/Compliance, acompanhados de seus respectivos Business Stewards e de um Technical Steward transversal) e operacional (Data Custodians/DBA, Engenharia de Dados, Segurança da Informação e Data Champions). Ligue os blocos com conectores que indiquem hierarquia (estratégica → tática → operacional) e relações de colaboração horizontal entre Data Owner e Business Steward da mesma área.

Para cada papel, escreva no próprio bloco do diagrama uma frase curta de até 15 palavras descrevendo a responsabilidade principal (ex.: "Define regras de negócio e aprova acessos no domínio Crédito").

Em uma planilha Excel chamada 01_papeis_swiftbank.xlsx, crie a aba Papéis com colunas: papel, camada, responsabilidade_principal, autoridade, tipo (formal/natural), exemplo_no_swiftbank. Preencha pelo menos 12 linhas, incluindo pelo menos um Data Champion (papel natural) e diferenciando Business Steward de Technical Steward em linhas separadas. Exporte o organograma do Draw.io como PNG e cole na aba Diagrama da mesma planilha.

Ferramentas: Draw.io, Excel.

Dicas de troubleshooting para a 1ª etapa:

Se o diagrama estiver "estourando" para fora da página, use o botão de ajuste de janela do Draw.io e revise se algum bloco foi arrastado para uma página secundária.
Cuidado para não confundir cargo (ex.: "Gerente de Crédito") com papel (ex.: "Data Owner do domínio Crédito"), a mesma pessoa pode ocupar um cargo e exercer um ou mais papéis.
Alguns papéis podem atravessar camadas na prática (por exemplo, Segurança da Informação tem CISO no estratégico e SecOps no operacional). Posicione o papel na camada onde ele atua predominantemente e justifique sua escolha em uma célula da coluna responsabilidade_principal ou em uma observação na planilha.

# 2ª Etapa: Ciclo de vida dos dados aplicado ao caso

Discutir no fórum
Agora você precisa mostrar, na prática, como um dado nasce, evolui e é descartado dentro do SwiftBank. O caso escolhido é o do conceito "Cliente Ativo", que hoje é definido de formas diferentes em Marketing, Crédito e Financeiro. Você produzirá um fluxograma do ciclo de vida cobrindo coleta → armazenamento → recuperação → uso → descarte, com responsáveis e perguntas-chave em cada etapa, mais um documento de apoio.

Pergunta-chave: "Quais decisões de governança precisam acontecer em cada etapa do ciclo de vida do dado de 'Cliente Ativo' para que ele possa ser usado de forma segura, consistente e em conformidade com a LGPD?"

Sua missão:

No Draw.io, crie um fluxograma horizontal com as cinco etapas do ciclo de vida (coleta, armazenamento, recuperação, uso, descarte). Em cada etapa, inclua: (a) os atores envolvidos (ex.: Engenharia de Dados, Data Owner, Segurança), (b) duas a três perguntas-chave (ex.: "temos direito de coletar?", "qual a finalidade declarada?", "quando descartar?") e (c) um exemplo concreto aplicado ao SwiftBank usando o dataset clientes_swiftbank.csv (ex.: na coleta, como entra o campo consentimento_marketing).
Em um documento Excel chamado 02_ciclo_de_vida_cliente_ativo.xlsx, crie a aba Etapas com colunas: etapa, acao, atores, perguntas_chave, riscos_LGPD, evidencia_no_dataset. Preencha uma linha por etapa, citando explicitamente onde no dataset cada etapa se materializa. Crie também a aba Camadas mostrando como o dado de "cliente" passa pelas camadas bronze (bz_clientes), silver (sl_clientes) e gold (gd_clientes_ativos), descrevendo o que muda em cada uma.
Crie a aba Definicao_Cliente_Ativo com a regra padronizada (ex.: "Cliente PF ou PJ com status_conta = Ativa e ao menos uma transação efetivada nos últimos 90 dias"), justificando por que essa regra elimina divergências entre Marketing, Crédito e Financeiro. Liste pelo menos três decisões erradas que aconteceriam sem essa padronização.
Ferramentas: Draw.io, Excel.

Dicas de troubleshooting para a 2ª etapa:

Se você travar para diferenciar "armazenamento" de "recuperação", lembre-se: armazenar é guardar; recuperar é localizar, pedir acesso e extrair. Quem aprova é o Data Owner.
Não confunda descarte com arquivamento. Pela LGPD, manter dado pessoal além da finalidade é problema; descarte exige procedimento, não basta apagar de uma planilha.
Se você não souber se um campo é dado pessoal sensível, consulte o clientes_swiftbank.csv: combinações de nome + cidade + data de nascimento já configuram identificação indireta.

# 3ª Etapa: Política de Acesso e Qualidade de Dados com indicadores e plano de implantação

Discutir no fórum
Com papéis e ciclo de vida mapeados, é hora de redigir a Política de Acesso e Qualidade de Dados de Clientes do SwiftBank, contendo os cinco elementos exigidos (propósito, escopo, papéis e responsabilidades, diretrizes e conformidade/exceções), além do plano de implantação e dos indicadores de monitoramento. Esse artefato será discutido no comitê de governança e servirá de referência para auditorias.

Pergunta-chave: "Como transformar acordos verbais sobre uso de dados de clientes em uma política prática, mensurável e auditável, sem virar burocracia?"

Sua missão:

Em um documento Excel chamado 03_politica_acesso_qualidade.xlsx, crie a aba Política com seções claramente identificadas em colunas (elemento, conteudo): Propósito, Escopo (sistemas, áreas, tipos de dados que cobre e que NÃO cobre), Papéis e Responsabilidades (CDO, DGO, Data Owners por domínio, Data Stewards, Data Custodians, Usuários, Data Champions), Diretrizes (ao menos 6 diretrizes operacionais, cada uma com responsável, frequência, sistema de registro e consequência de descumprimento) e Conformidade/Exceções (como exceções são solicitadas e quem aprova). Use um assistente de IA generativa (ChatGPT, Claude, Gemini ou similar) como apoio para revisar redação, mas valide cada diretriz: ela precisa ser específica, mensurável e ter responsável.
Crie a aba Plano_Implantacao com três passos (comunicação direcionada, responsáveis e cronograma, integração com metas e rituais), descrevendo ações concretas para o SwiftBank, ex.: workshop com Marketing antes do go-live, reunião quinzenal com Data Champions, indicador de qualidade entrando no OKR trimestral da diretoria de Crédito. Crie também a aba Indicadores com pelo menos cinco métricas (ex.: % de dados mestres atualizados no prazo, número de inconsistências por mês, % de áreas que cumprem revisão, tempo médio de correção, engajamento em treinamentos), cada uma com fórmula, fonte do dado, meta e responsável.
Crie a aba Cenarios_Diagnostico com pelo menos três cenários narrados (ex.: compartilhamento de base com consultoria terceirizada de cobrança, dúvida entre Marketing e Crédito sobre consentimento_marketing, pedido emergencial de extração da base de empréstimos). Para cada cenário, identifique: política aplicável, falhas que poderiam ocorrer sem ela, papéis envolvidos e ações corretivas esperadas. Marque qual diretriz da aba Política previne cada caso.
Ferramentas: Excel, assistente de IA generativa (ChatGPT, Claude, Gemini ou similar).

Dicas de troubleshooting para a 3ª etapa:

Se uma diretriz começa com verbos como "zelar", "garantir" ou "buscar" sem complemento, ela está vaga. Refaça respondendo: o quê, quem, com que frequência, onde se registra, qual a consequência?
Cuidado ao usar assistentes de IA: não cole dados reais, e revise sempre a saída. O LLM pode inventar regulamentos ou inverter responsabilidades entre Owner e Steward.
Se você tiver mais de 12 diretrizes na Política, considere mover algumas para um documento de "Procedimento". Política diz o quê, procedimento diz o como.

# 4ª Etapa: Glossário de negócio, dicionário de dados e diagnóstico de qualidade de metadados

Discutir no fórum
A etapa de fechamento integra tudo o que foi feito antes: você entregará o glossário de negócio inicial do SwiftBank, o dicionário de dados das tabelas de Cliente, Transações e Empréstimos, um esboço de linhagem entre tabelas (bronze → silver → gold) e um diagnóstico de qualidade dos metadados existentes (usando o metadados_tabelas_swiftbank.csv). Aqui, e somente aqui, entra um pequeno script em Python para apoiar o diagnóstico, já que medir completude de metadados em 38 linhas manualmente é viável, mas a equipe quer um padrão replicável para crescer no futuro.

Pergunta-chave: "Como entregar, em um único pacote, um glossário, um dicionário de dados, uma linhagem e um diagnóstico de metadados que permita ao SwiftBank começar a falar a mesma língua sobre seus dados?"

Sua missão:

Em um arquivo Excel chamado 04_glossario_e_dicionario.xlsx, crie a aba Glossario com pelo menos 12 termos de negócio do SwiftBank (ex.: Cliente Ativo, Cliente PF, Cliente PJ, Conta Corrente, Empréstimo, Score de Crédito, Apólice, Transação Efetivada, Receita, Inadimplência, Dado Pessoal Sensível, Consentimento de Marketing). Cada termo deve ter: nome, definicao, contexto_de_uso, responsavel (Owner), domínio, termos_relacionados e status (rascunho/aprovado). Crie a aba Dicionario_Dados com uma linha por coluna das tabelas presentes no metadados_tabelas_swiftbank.csv e do clientes_swiftbank.csv, agrupando por tabela e camada. Crie a aba Linhagem descrevendo de forma textual a relação bz_clientes → sl_clientes → gd_clientes_ativos e bz_transacoes → sl_transacoes → gd_metricas_credito, indicando quais transformações ocorrem (ex.: cálculo de idade, harmonização de moeda, criação de flag_ativo).
No Draw.io, faça um diagrama de linhagem visual (caixas e setas) mostrando as tabelas das três camadas e indicando, em cada seta, a transformação aplicada. Exporte como PNG e inclua em uma aba Diagrama_Linhagem do mesmo Excel.
No Google Colab, escreva um pequeno script em Python com Pandas que leia o metadados_tabelas_swiftbank.csv e calcule: (a) % de completude de cada coluna (descricao, confidencialidade, dado_pessoal, responsavel); (b) quantas linhas têm camada fora da lista permitida (bronze, silver, gold); (c) quantas descrições possuem 3 palavras ou menos; (d) ranking das tabelas com pior qualidade de metadados. Salve o resultado em uma aba Diagnostico_Metadados do Excel (pode copiar e colar o output) com um parágrafo de leitura de negócio: quais 3 tabelas devem ser priorizadas para correção e por quê. Por fim, em uma aba Plano_Acao, vincule cada problema encontrado a um responsável (Owner/Steward), prazo e diretriz da política da 3ª etapa.
Ferramentas: Excel, Draw.io, Google Colab, Python, Pandas, assistente de IA generativa (ChatGPT, Claude, Gemini ou similar).

Dicas de troubleshooting para a 4ª etapa:

Se o pd.read_csv quebrar com acentos, especifique encoding='utf-8'. Se o separador for diferente, use sep=',' ou ajuste conforme o arquivo carregado no Colab.
Para medir completude, lembre-se de tratar células vazias como nulos: df['coluna'].isna().sum() ou comparar com strings vazias após df.fillna('').
Se duas descrições do mesmo nome de coluna divergirem entre tabelas (ex.: data_referencia significando coisas diferentes em gd_clientes_ativos e gd_metricas_credito), isso é um problema de glossário, não de Python, registre na aba Plano_Acao.
Cuidado ao apresentar o diagnóstico: o objetivo não é apontar culpados, mas mobilizar Owners e Stewards. Use linguagem de accountability, não de culpa.



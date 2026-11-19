# Citizen Assist AI — Carreiras em Ciência da Computação

**Global Solution 2026.2 — Pensamento Computacional e Automação com Python | FIAP**

## 1. Equipe e apresentação

### Integrantes

| Integrante | RM |
|---|---|
| David Gabriel | 574147 |
| Enzo Christino | 572047 |
| João Lucas | 571355 |

**Vídeo técnico:** [Assistir à apresentação no YouTube](https://youtu.be/ruzG0CyacgQ)

**Público-alvo:** Estudantes de Ciência da Computação e pessoas que estão iniciando uma carreira na área de tecnologia.

**ODS relacionados:**
- ODS 4 — Educação de Qualidade.
- ODS 8 — Trabalho Decente e Crescimento Econômico.

### Problema identificado

Estudantes que estão começando na área de tecnologia frequentemente encontram dificuldades para localizar informações confiáveis sobre como estudar programação, conhecer profissões, procurar estágios, desenvolver projetos e montar um portfólio.

Essas informações estão distribuídas entre diferentes sites, documentos e plataformas, dificultando o acesso a orientações organizadas e verificáveis.

### Solução desenvolvida

O **Citizen Assist AI** é um assistente desenvolvido em Python que oferece orientações sobre formação e carreira em Ciência da Computação.

O sistema permite que o usuário faça perguntas e receba respostas fundamentadas em uma base de conhecimento local, incluindo fontes e datas de verificação.

O projeto utiliza **busca baseada em regras e pontuação**, sem modelos de inteligência artificial generativa.

A base possui **12 orientações distribuídas em 3 categorias**. Também foi desenvolvida uma interface HTML complementar, com um chatbot para participantes e um painel de estatísticas para o operador.

---

## 2. Tecnologias utilizadas

O projeto foi desenvolvido utilizando:

- **Python 3:** lógica principal, orientação a objetos, processamento de perguntas e indicadores.
- **JSON:** armazenamento da base de conhecimento e do histórico de atendimentos.
- **CSV:** exportação dos registros para análise.
- **HTML, CSS e JavaScript:** interface web complementar.
- **Biblioteca padrão do Python:** manipulação de arquivos, expressões regulares, datas, horários e servidor HTTP local.

Não é necessário instalar bibliotecas externas.

---

## 3. Como executar o projeto

### 3.1. Executar no terminal

Abra a pasta que contém `main.py` no VS Code ou em outro editor.

No terminal, execute:

```bash
python3 main.py
```

No Windows, também pode funcionar:

```bash
python main.py
```

O programa apresenta o seguinte menu:

```text
===== Citizen Assist AI =====

1 - Digitar uma dúvida
2 - Navegar por categorias
3 - Ver indicadores
0 - Sair
```

As entradas inválidas são tratadas sem encerrar o programa inesperadamente.

### 3.2. Executar a interface web

Na mesma pasta do projeto, execute:

```bash
python3 web_app.py
```

Com o servidor aberto, acesse:

**Página inicial:**

http://127.0.0.1:8000/

**Chat do participante:**

http://127.0.0.1:8000/usuario

**Chat e estatísticas do operador:**

http://127.0.0.1:8000/operador

**Observação:** a interface web funciona localmente e depende do servidor Python. Não é possível utilizar todas as funcionalidades abrindo diretamente o arquivo HTML.

---

## 4. Estrutura do projeto

```text
citizen-assist-ai/
├── README.md
├── main.py
├── orientacao.py
├── base_conhecimento.py
├── assistente.py
├── web_app.py
├── web/
│   └── index.html
└── data/
    ├── base_conhecimento.json
    ├── historico.json
    └── atendimentos.csv
```

### Responsabilidade dos arquivos

**`main.py`**

Responsável por iniciar o programa e apresentar o menu principal de navegação no terminal.

**`orientacao.py`**

Contém a classe `Orientacao`, responsável por representar uma orientação individual.

**`base_conhecimento.py`**

Contém a classe `BaseConhecimento`, responsável pelo carregamento do JSON, organização por categorias e busca por pontuação.

**`assistente.py`**

Contém a classe `Assistente`, responsável pelas interações, histórico, avaliações, indicadores e exportação CSV.

**`web_app.py`**

Disponibiliza um servidor HTTP local que conecta a interface HTML à lógica desenvolvida em Python.

**`web/index.html`**

Contém a interface do chatbot e o painel do operador.

**`data/base_conhecimento.json`**

Armazena as orientações consultadas pelo programa.

**`data/historico.json`**

Armazena os atendimentos realizados.

**`data/atendimentos.csv`**

Contém a exportação dos registros de atendimento em formato tabular.

---

## 5. Orientação a objetos

O projeto utiliza três classes principais.

### Classe `Orientacao`

Representa uma orientação individual da base de conhecimento.

Seus principais atributos são:

- `id`
- `categoria`
- `titulo`
- `palavras_chave`
- `resposta`
- `documentos`
- `onde`
- `fonte`
- `verificado_em`

O método `exibir()` apresenta as informações no terminal.

### Classe `BaseConhecimento`

Responsável por carregar e organizar os registros.

Seus principais métodos são:

- `carregar()`
- `categorias()`
- `por_categoria()`
- `pontuar()`
- `buscar()`

### Classe `Assistente`

Responsável pelo funcionamento dos atendimentos.

Seus principais métodos incluem:

- `perguntar()`
- `navegar()`
- `registrar()`
- `indicadores()`
- `resumo_indicadores()`
- `avaliar_facilidade()`
- `exportar_csv()`

### Composição entre as classes

O sistema utiliza composição para relacionar os objetos:

```text
Assistente
  └── BaseConhecimento
        └── Lista de objetos Orientacao
```

A classe `Assistente` utiliza um objeto da classe `BaseConhecimento`, que armazena uma lista de objetos `Orientacao`.

---

## 6. Base de conhecimento

A base de conhecimento está localizada em:

`data/base_conhecimento.json`

O arquivo contém **12 orientações**, organizadas em três categorias:

### Formação e estudos

- Começar a estudar programação com Python.
- Encontrar cursos gratuitos de tecnologia no Aprenda Mais, do MEC.
- Conferir cursos de Ciência da Computação no e-MEC.
- Organizar uma rotina inicial de estudos de programação.

### Carreira e primeiro emprego

- Conhecer profissões e ocupações da área de TI.
- Entender as regras de estágio em Ciência da Computação.
- Obter a Carteira de Trabalho Digital.
- Pesquisar vagas no SINE e no Emprega Brasil.

### Projetos e portfólio

- Criar um repositório de portfólio no GitHub.
- Escrever um README para um projeto de programação.
- Escolher um projeto inicial para praticar Python.
- Entender o registro de software no INPI.

Cada registro possui os campos obrigatórios definidos no enunciado, incluindo pelo menos três palavras-chave, resposta, documentos ou requisitos, local de consulta, fonte e data de verificação.

---

## 7. Funcionamento da busca e pontuação

A busca utiliza a função `normalizar()` para padronizar os textos.

Essa função:

1. Converte os caracteres para minúsculas.
2. Remove acentos.
3. Remove pontuação.
4. Elimina espaços desnecessários.

Depois da normalização, o método `pontuar()` compara a pergunta com cada orientação.

### Regras de pontuação

- **+3 pontos:** para cada palavra-chave ou expressão completa da orientação encontrada na pergunta.
- **+1 ponto:** para cada palavra distinta da pergunta com quatro ou mais letras que também apareça no título da orientação.

O método `buscar()` retorna uma lista de tuplas no formato:

```python
(pontos, orientacao)
```

As tuplas são ordenadas da maior pontuação para a menor.

### Classificação de confiança

| Pontuação | Confiança |
|---|---|
| 6 pontos ou mais | ALTA |
| De 3 a 5 pontos | MÉDIA |
| Menos de 3 pontos | Não encontrada |

O programa apresenta a orientação mais bem pontuada e até duas alternativas relevantes.

Na navegação direta por categorias, a classificação de confiança não se aplica.

---

## 8. Privacidade e tratamento de entradas

O sistema não solicita nome, CPF, telefone ou e-mail dos participantes.

Para permitir a contagem dos usuários durante os testes, a interface gera um identificador anônimo por sessão, como:

```text
P-A1B2C3
```

O programa também bloqueia perguntas que contenham:

- O caractere `@`.
- Oito ou mais dígitos numéricos.

Essas perguntas são recusadas e não entram no histórico.

O sistema também trata entradas vazias, opções inválidas e avaliações fora das alternativas permitidas.

As respostas apresentam a fonte, a data de verificação e um aviso de que o assistente não representa um canal oficial.

---

## 9. Histórico e indicadores

Os atendimentos são registrados em:

`data/historico.json`

Cada registro contém informações como:

- Data do atendimento.
- Origem da consulta.
- Pergunta realizada.
- Identificador da orientação.
- Resultado da busca.
- Avaliação de utilidade.
- Quantidade de tentativas.
- Tempo gasto em segundos.
- Identificador anônimo do participante.

O tempo é medido utilizando `time.time()`.

Os registros também podem ser exportados para:

`data/atendimentos.csv`

A exportação utiliza `csv.DictWriter`.

### Indicadores calculados

- Quantidade de atendimentos.
- Quantidade de participantes.
- Percentual de respostas encontradas.
- Taxa de respostas consideradas úteis.
- Tempo médio para encontrar uma orientação.
- Média de tentativas por atendimento.
- Facilidade de uso, em escala de 1 a 5.
- Dúvidas sem solução.

O painel do operador apresenta os indicadores e o histórico dos participantes.

As interações realizadas no terminal para demonstração são separadas dos resultados dos testes com usuários externos.

---

## 10. Testes reais com usuários

**Data dos testes:** 15 de novembro de 2026.

Foram registrados **3 participantes identificados por códigos anônimos** e **10 atendimentos concluídos** no modo de teste.

Os participantes realizaram 11 perguntas válidas no total, pois um dos atendimentos exigiu reformulação.

Cinco atendimentos foram realizados por perguntas em texto livre e cinco pela navegação entre categorias.

### Resultados obtidos

| Indicador | Resultado |
|---|---:|
| Participantes distintos | 3 |
| Atendimentos concluídos | 10 |
| Perguntas válidas | 11 |
| Respostas encontradas | 100,0% |
| Respostas consideradas úteis | 60,0% |
| Tempo médio para encontrar uma orientação | 30,4 segundos |
| Média de tentativas por atendimento | 1,1 |
| Avaliações positivas | 6 |
| Avaliações negativas | 4 |
| Facilidade de uso (1 a 5) | Não disponível |

### Interpretação dos resultados

Todos os dez atendimentos foram concluídos com uma orientação encontrada.

Entretanto, **100% de respostas encontradas não significa 100% de satisfação ou assertividade**.

Dos dez atendimentos, seis orientações foram consideradas úteis pelos participantes, enquanto quatro foram avaliadas como não úteis.

O percentual de respostas encontradas também inclui os atendimentos realizados por navegação direta nas categorias.

### Dúvidas que não foram resolvidas satisfatoriamente

Quatro orientações foram encontradas, mas avaliadas como não úteis:

1. **Como começar a estudar Python?**
2. **Quais profissões existem na área de tecnologia?**
3. **Conferir curso de Ciência da Computação no e-MEC.**
4. **Organizar uma rotina inicial de estudo de programação.**

Essas perguntas receberam respostas do programa, porém não atenderam às expectativas dos participantes.

Como não foram registradas justificativas textuais das avaliações negativas, não é possível determinar com precisão o motivo de cada uma.

### Facilidade de uso

A aplicação possui uma avaliação de facilidade de uso em escala de 1 a 5.

Entretanto, os arquivos dos testes enviados não apresentam notas registradas nesse campo.

Por esse motivo, o indicador foi mantido como **não disponível**, sem atribuição de valores estimados.

---

## 11. Melhoria implementada após os testes

Durante os testes, um participante utilizou inicialmente a pergunta:

> Como estudar código da melhor forma?

A pergunta não atingiu a pontuação mínima necessária para encontrar uma orientação confiável.

O participante precisou reformular a dúvida para:

> O que estudar primeiro na área de tecnologia?

Esse atendimento exigiu duas tentativas e registrou um tempo de 132,2 segundos.

### Problema identificado

A base de conhecimento possuía uma orientação relacionada à organização dos estudos, mas não reconhecia a primeira formulação utilizada pelo participante.

### Melhoria realizada

Foi adicionada a expressão:

```json
"como estudar codigo da melhor forma"
```

À lista `palavras_chave` da orientação de ID 4:

**Organizar uma rotina inicial de estudo de programação.**

### Resultado da melhoria

**Antes da alteração:**

A pergunta original não atingia o mínimo de três pontos necessário para apresentar uma orientação.

**Depois da alteração:**

A mesma pergunta passou a encontrar a orientação correspondente com **3 pontos e confiança MÉDIA**.

A melhoria foi verificada por meio da função de busca do programa.

Os indicadores apresentados neste README continuam representando os testes originais, sem inclusão de atendimentos ou avaliações fictícias após a alteração.

---

## 12. Fontes consultadas

As orientações utilizam fontes oficiais de serviços públicos ou documentações mantidas pelos responsáveis pelas tecnologias.

| Assunto | Fonte |
|---|---|
| Aprendizado de Python | [Python Docs](https://docs.python.org/pt-br/3/tutorial/) |
| Cursos gratuitos | [MEC — Aprenda Mais](https://aprendamais.mec.gov.br/course/index.php?lang=pt_br) |
| Consulta de cursos superiores | [MEC — Cadastro e-MEC](https://www.gov.br/mec/pt-br/politica-regulacao-supervisao-educacao-superior/cadastro-nacional-de-cursos-e-ies) |
| Rotina de estudos de programação | [Python Docs](https://docs.python.org/pt-br/3/tutorial/) |
| Profissões da área de TI | [Ministério do Trabalho — CBO](https://www.gov.br/trabalho-e-emprego/pt-br/assuntos/cbo) |
| Regras de estágio | [Ministério do Trabalho](https://www.gov.br/trabalho-e-emprego/pt-br/acesso-a-informacao/acoes-e-programas/programas-projetos-acoes-obras-e-atividades/proteja/duvidas-frequentes/duvidas-frequentes) |
| Carteira de Trabalho Digital | [Gov.br](https://www.gov.br/pt-br/servicos/obter-a-carteira-de-trabalho) |
| Busca de emprego pelo SINE | [Gov.br](https://www.gov.br/pt-br/servicos/buscar-emprego-no-sistema-nacional-de-emprego-sine) |
| Repositórios do GitHub | [GitHub Docs](https://docs.github.com/pt/repositories) |
| Documentação README | [GitHub Docs](https://docs.github.com/pt/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/quickstart-for-writing-on-github) |
| Projetos iniciais com Python | [Python Docs](https://docs.python.org/pt-br/3/tutorial/) |
| Registro de software | [INPI — Gov.br](https://www.gov.br/pt-br/servicos/solicitar-o-registro-de-programa-de-computador) |

**Data de verificação das orientações:** 15/11/2026.

As recomendações sobre rotina de estudos e projetos são sugestões didáticas, não normas governamentais.

---

## 13. Decisões técnicas e limitações

### Decisão técnica

A principal decisão técnica foi utilizar uma base JSON com busca por pontuação, em vez de integrar um modelo generativo.

Essa escolha permite compreender e explicar como cada orientação é encontrada, utilizar conteúdos estruturados e apresentar as fontes utilizadas.

### Limitações identificadas

- A busca depende de palavras-chave e pode não reconhecer perguntas formuladas de maneiras diferentes.
- O nível de confiança representa correspondência textual, não garantia de que a orientação resolverá a dúvida.
- As informações precisam ser revisadas periodicamente, pois o sistema não atualiza automaticamente as fontes pela internet.
- A interface web foi desenvolvida para execução local.
- A página do operador não utiliza autenticação e não deve ser publicada como um painel aberto na internet.
- O bloqueio de dados pessoais atende à regra programada, mas não identifica todos os tipos possíveis de informação pessoal.
- A nota de facilidade de uso não foi registrada nos testes atuais.

---

## 14. Integração com outras disciplinas

Não foram utilizadas integrações com outras disciplinas.

A interface HTML funciona como um complemento visual ao projeto de Python e utiliza a mesma lógica de busca e pontuação do programa em terminal.

---

## 15. Vídeo técnico

A equipe gravou um vídeo técnico apresentando a implementação do Citizen Assist AI.

A demonstração aborda a estrutura JSON, os conceitos de orientação a objetos, a normalização das perguntas, a pontuação, o funcionamento no terminal, a alteração de uma palavra-chave, o histórico, os indicadores e as limitações do projeto.

**[Assistir ao vídeo técnico no YouTube](https://youtu.be/ruzG0CyacgQ)**

---

## 16. Considerações finais

O Citizen Assist AI permitiu aplicar conceitos de programação Python, orientação a objetos, estruturas de dados, manipulação de arquivos e processamento de textos.

Os testes com usuários ajudaram a identificar limitações da busca textual e oportunidades de melhoria na base de conhecimento.

Como resultado, foi desenvolvido um assistente funcional, com respostas fundamentadas em fontes identificadas, histórico de atendimentos e indicadores que permitem avaliar sua utilização.

O projeto demonstra como uma solução baseada em regras pode organizar informações e auxiliar estudantes em suas primeiras decisões relacionadas à formação e à carreira em Ciência da Computação.

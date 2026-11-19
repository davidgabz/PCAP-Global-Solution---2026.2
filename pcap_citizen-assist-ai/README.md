# Citizen Assist AI — Carreiras em Ciência da Computação

**Global Solution 2026.2 — Pensamento Computacional e Automação com Python (FIAP)**

## 1. Equipe e apresentação

**Integrantes:**

- David Gabriel — RM 574147
- Enzo Christino — RM 572047
- João Lucas — RM 571355

**Vídeo técnico (YouTube, não listado):** https://youtu.be/ruzG0CyacgQ  

**Público escolhido:** estudantes de Ciência da Computação e pessoas iniciando a carreira na área de tecnologia.  
**Problema:** orientações sobre estudos, estágio, profissões, documentos, projetos e portfólio estão espalhadas entre sites diferentes e nem sempre são fáceis de localizar.  
**Solução:** assistente em Python que responde perguntas a partir de uma base JSON de orientações com fonte e data de verificação.  
**ODS relacionados:** ODS 4 — Educação de Qualidade; ODS 8 — Trabalho Decente e Crescimento Econômico.

O assistente utiliza **busca por regras**, não modelos de IA generativa. As respostas são limitadas ao conteúdo da base de conhecimento. Há 12 orientações distribuídas em 3 categorias. A interface HTML é um complemento; a execução no terminal continua disponível para a avaliação de Python.

## 2. Como executar

É necessário **Python 3**. O projeto não depende de bibliotecas externas.

**Terminal (modo obrigatório da disciplina):** abra o terminal na pasta `citizen-assist-ai` e execute:

```bash
python3 main.py
```

No Windows, também pode funcionar `python main.py` ou `py main.py`.

O menu oferece: `1` digitar uma dúvida, `2` navegar por categorias, `3` visualizar indicadores e `0` sair. Opções inválidas são tratadas sem encerrar o programa.

**Interface web local (opcional):** no terminal, execute:

```bash
python3 web_app.py
```

Com o servidor aberto, acesse:

- `http://127.0.0.1:8000/` — página inicial;
- `http://127.0.0.1:8000/usuario` — chat do participante;
- `http://127.0.0.1:8000/operador` — chat e indicadores do operador.

**Não abra** `web/index.html` diretamente no navegador: a interface depende do servidor Python local.

## 3. Estrutura dos arquivos

```text
citizen-assist-ai/
├── README.md
├── main.py
├── orientacao.py
├── base_conhecimento.py
├── assistente.py
├── web_app.py                  # interface adicional
├── web/
│   └── index.html             # interface adicional
└── data/
    ├── base_conhecimento.json
    ├── historico.json
    └── atendimentos.csv
```

### Classes obrigatórias

- **`Orientacao` (`orientacao.py`):** recebe os campos de um registro JSON (`id`, `categoria`, `titulo`, `palavras_chave`, `resposta`, `documentos`, `onde`, `fonte`, `verificado_em`) e os apresenta com `exibir()`.
- **`BaseConhecimento` (`base_conhecimento.py`):** mantém `caminho` e `orientacoes` (lista de objetos `Orientacao`); usa `carregar()`, `categorias()`, `por_categoria()`, `pontuar()` e `buscar()`.
- **`Assistente` (`assistente.py`):** mantém o nome, a base de conhecimento e o histórico; controla perguntas, navegação, registro, indicadores e exportação CSV.

As classes se relacionam por **composição**:

```text
Assistente
  └── base: BaseConhecimento
        └── orientacoes: [Orientacao, Orientacao, ...]
```

`main.py` cria a base, chama `base.carregar()`, cria o assistente e apresenta o menu.

## 4. Base de conhecimento e fontes

O arquivo `data/base_conhecimento.json` contém **12 orientações**, divididas em **3 categorias**: Formação e estudos; Carreira e primeiro emprego; Projetos e portfólio. Cada orientação contém os nove campos obrigatórios, ao menos três palavras-chave, resposta em linguagem simples, fonte e data de verificação.

As fontes são páginas oficiais de serviços públicos ou a documentação dos responsáveis pelas tecnologias citadas. Orientações de rotina de estudos e projetos são **sugestões didáticas**, não regras governamentais.

### Fontes consultadas

- **01 — Começar a estudar programação com Python**: https://docs.python.org/pt-br/3/tutorial/ (conferido em 2026-11-15)
- **02 — Encontrar cursos gratuitos de tecnologia no Aprenda Mais (MEC)**: https://aprendamais.mec.gov.br/course/index.php?lang=pt_br (conferido em 2026-11-15)
- **03 — Conferir curso de Ciência da Computação no e-MEC**: https://www.gov.br/mec/pt-br/politica-regulacao-supervisao-educacao-superior/cadastro-nacional-de-cursos-e-ies (conferido em 2026-11-15)
- **04 — Organizar uma rotina inicial de estudo de programação**: https://docs.python.org/pt-br/3/tutorial/ (conferido em 2026-11-15)
- **05 — Conhecer profissões e ocupações da área de TI**: https://www.gov.br/trabalho-e-emprego/pt-br/assuntos/cbo (conferido em 2026-11-15)
- **06 — Entender as regras de estágio em Ciência da Computação**: https://www.gov.br/trabalho-e-emprego/pt-br/acesso-a-informacao/acoes-e-programas/programas-projetos-acoes-obras-e-atividades/proteja/duvidas-frequentes/duvidas-frequentes (conferido em 2026-11-15)
- **07 — Obter a Carteira de Trabalho Digital para o primeiro emprego**: https://www.gov.br/pt-br/servicos/obter-a-carteira-de-trabalho (conferido em 2026-11-15)
- **08 — Pesquisar vagas no SINE e no Emprega Brasil**: https://www.gov.br/pt-br/servicos/buscar-emprego-no-sistema-nacional-de-emprego-sine (conferido em 2026-11-15)
- **09 — Criar um repositório de portfólio no GitHub**: https://docs.github.com/pt/repositories (conferido em 2026-11-15)
- **10 — Escrever um README claro para um projeto de programação**: https://docs.github.com/pt/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/quickstart-for-writing-on-github (conferido em 2026-11-15)
- **11 — Escolher um projeto inicial para praticar Python**: https://docs.python.org/pt-br/3/tutorial/ (conferido em 2026-11-15)
- **12 — Entender o registro de software no INPI**: https://www.gov.br/pt-br/servicos/solicitar-o-registro-de-programa-de-computador (conferido em 2026-11-15)

## 5. Regra de pontuação e confiança

A função `normalizar()` converte os textos para minúsculas e remove acentos, pontuação e espaços extras. Depois, `pontuar()` aplica:

- **+3 pontos** para cada palavra-chave ou expressão completa da orientação encontrada na pergunta;
- **+1 ponto** para cada palavra distinta da pergunta com quatro letras ou mais que também apareça no título.

`buscar()` devolve **tuplas** `(pontos, orientacao)` ordenadas da maior pontuação para a menor. O sistema mostra a melhor orientação e até duas alternativas pertinentes.

- **ALTA:** 6 pontos ou mais;
- **MÉDIA:** entre 3 e 5 pontos;
- **Não encontrada:** menos de 3 pontos; sugere reformular a pergunta ou navegar por categorias.

Na navegação direta por categorias, a confiança por busca não se aplica.

## 6. Atendimento, privacidade, histórico e CSV

- O programa trata perguntas vazias, opções fora do intervalo e respostas `s/n` inválidas, sem encerrar inesperadamente.
- Não pede nome, CPF, telefone nem e-mail aos participantes. Perguntas contendo `@` ou **8 ou mais dígitos** são recusadas, sem registro.
- Cada participante web recebe um ID de sessão anônimo (`P-XXXXXX`); nomes não são armazenados.
- Toda orientação informa título, resposta, documentos/requisitos, onde consultar, **fonte, data de verificação** e aviso de que **este assistente não é canal oficial**.
- Os atendimentos são registrados em `data/historico.json` com data, origem, pergunta, ID da orientação, encontrou, ajudou, tentativas e tempo em segundos (além de campos auxiliares).
- O tempo é calculado com `time.time()` e o CSV é exportado com `csv.DictWriter` para `data/atendimentos.csv`.

O painel do operador mostra respostas encontradas (%), taxa de acerto/ajudou (%), tempo médio, tentativas por atendimento, facilidade de uso (1 a 5), dúvidas sem solução, histórico por sessão e exportação CSV. As conversas de demonstração no terminal não são contabilizadas nos indicadores dos participantes externos.

## 7. Testes reais com usuários — 15/11/2026

O sistema foi utilizado em **3 sessões de participantes identificados por códigos anônimos** e gerou **10 atendimentos concluídos** no modo `teste`. Foram **11 perguntas válidas**, porque um atendimento exigiu uma reformulação. Cinco atendimentos foram feitos por pergunta em texto livre e cinco por navegação em categorias.

A análise usa somente os registros `modo: "teste"`. O `historico.json` também contém **3 atendimentos adicionais de demonstração no terminal**, que não entram nos indicadores abaixo. O CSV do pacote final contém os 13 registros (10 de teste e 3 do terminal), conforme a exportação padrão do programa; use a coluna `modo` para distinguir os dois grupos.

| Indicador exigido | Resultado observado |
|---|---:|
| Participantes distintos (IDs de sessão) | **3** |
| Atendimentos de teste concluídos | **10** |
| Perguntas válidas, incluindo reformulações | **11** |
| Resposta encontrada (%) | **100,0%** (10/10) |
| Taxa de acerto — orientação ajudou (%) | **60,0%** (6/10) |
| Tempo médio para encontrar (respostas encontradas) | **30,4 segundos** |
| Tentativas por atendimento | **1,1** (11/10) |
| Facilidade de uso (1 a 5) | **Não disponível: nenhuma nota foi registrada** |
| Avaliações de utilidade positivas | **6** |
| Avaliações de utilidade negativas | **4** |

**Interpretação importante:** o percentual de 100% inclui as orientações selecionadas por categoria; **não** significa 100% de sucesso na busca por texto livre. A taxa de utilidade de 60% representa o julgamento dos participantes, não uma verificação automática da exatidão de todas as informações. Nenhum dos dez atendimentos foi encerrado sem uma orientação; quatro orientações encontradas foram avaliadas como **não úteis**.

### Dúvidas que não foram resolvidas satisfatoriamente

Os quatro registros com `ajudou: false` foram:

1. “Como começar a estudar Python?”
2. “Quais profissões existem na área de tecnologia?”
3. “Conferir curso de Ciência da Computação no e-MEC”
4. “Organizar uma rotina inicial de estudo de programação”

Essas dúvidas **receberam orientação**, mas os participantes avaliaram que **não ajudou**. Não há justificativas textuais registradas para as avaliações negativas, por isso não é possível afirmar a causa de cada uma.

### Melhoria implementada a partir dos testes (18/11/2026)

Durante um atendimento, o participante perguntou inicialmente **“Como estudar código da melhor forma?”**, que não atingiu a pontuação mínima de busca, e precisou reformular para **“O que estudar primeiro na área de tecnologia?”**. Esse atendimento teve duas tentativas e tempo de **132,2 segundos**.

Para tratar a dificuldade observada, foi adicionada a expressão **`"como estudar codigo da melhor forma"`** às `palavras_chave` da orientação **ID 4 — “Organizar uma rotina inicial de estudo de programação”**, no arquivo `data/base_conhecimento.json`.

- **Antes da alteração:** a pergunta original não atingia 3 pontos na melhor orientação.
- **Depois da alteração:** a orientação ID 4 passou a receber **3 pontos (confiança MÉDIA)** para a mesma pergunta.

A verificação após a alteração foi feita executando a função de busca do programa. **Não foram inventados novos atendimentos ou avaliações dos participantes:** todos os indicadores apresentados continuam sendo os resultados originais dos testes.

### Nota de facilidade pendente

A interface prevê avaliação da facilidade de uso de 1 a 5, mas **todos os registros enviados possuem `facilidade: null`**. Portanto, não foi calculada uma média. Caso a equipe ainda tenha avaliações reais anotadas, elas devem ser registradas com transparência; **não é correto preencher notas por estimativa**.

## 8. Integração com outras disciplinas

**Não foram utilizadas integrações com outras disciplinas.** Essa parte é opcional no enunciado. A interface HTML é apenas um complemento local e usa o mesmo algoritmo de pontuação do modo terminal.

## 9. Limitações

- A base responde apenas aos assuntos previamente cadastrados e depende de palavras-chave; pode não reconhecer uma pergunta válida escrita de outra forma.
- A confiança representa **correspondência textual**, não uma garantia de que a orientação solucionará a dúvida.
- As fontes precisam ser revisadas periodicamente; o sistema não consulta a internet automaticamente para atualizar respostas.
- A interface web funciona localmente. A rota do operador não exige login; portanto, **não é uma área protegida para publicação aberta na internet**.
- O bloqueio automático de dados pessoais segue a regra do enunciado (`@` ou 8 dígitos); não é um detector completo de todos os possíveis dados pessoais.
- A nota de facilidade não foi coletada nos dados atuais dos participantes.

## 10. Entrega e vídeo

**Vídeo técnico:** https://youtu.be/ruzG0CyacgQ
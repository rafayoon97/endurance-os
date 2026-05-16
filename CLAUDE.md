# endurance-os — Contexto do Projeto

## O que é

Plataforma pessoal de dados esportivos. Integra Strava + Apple Health, calcula 
métricas de carga de treino (CTL, ATL, ACWR, decoupling), gera relatórios 
semanais e tem um "treinador IA" que sugere ajustes.

É projeto de portfólio pra demonstrar competência como **AI Product Builder 
com fundamentos sólidos de dados**: ciclo de identificação de dor → modelagem 
de dados → prototipagem com IA → iteração baseada em uso real.

## Sobre o desenvolvedor

- **Posicionamento profissional:** AI Product Builder com fundamentos sólidos 
  de dados. Constrói produtos que resolvem dores reais, com uso intenso de 
  IA generativa, sobre base de modelagem de dados não trivial. Pensa sob 
  ótica de problema/dor antes de tecnologia.
- Faz scripts quando precisa, não é fluente em Python, mas topa aprender o 
  necessário pra construir.
- SQL e modelagem de dados são skills centrais que ele quer demonstrar e 
  aprofundar.
- Ambiente Windows.
- Tempo: 1-2h/dia, fragmentado.
- Balanço aprendizado/velocidade: 60/40 (implementação própria preferida onde 
  agrega skill demonstrável).

## Princípios de desenvolvimento

1. **Sempre executável**: o projeto nunca pode estar quebrado entre commits. 
   Refatorações grandes ficam em branches.

2. **Implementação própria onde tem valor analítico ou de produto**: OAuth, 
   schema SQL, métricas fisiológicas, prompts. Usar biblioteca onde é só 
   plumbing (pandas, Streamlit, plotly).

3. **Sem ORM**: SQL escrito à mão. Schema em `src/db/schema.sql`. Views 
   analíticas em `src/db/views.sql`. Queries parametrizadas em arquivos 
   `.sql` separados sob `src/db/queries/`, não strings embutidas em Python.

4. **SQL é cidadão de primeira classe**: quando uma análise pode ser feita 
   tanto em SQL quanto em pandas, preferir SQL (com window functions, CTEs, 
   views). Pandas entra para transformações que SQL não faz bem.

5. **Privacidade**: dados pessoais NUNCA são commitados. Banco SQLite, XML do 
   Apple Health, .env, athlete_profile.yaml → todos no .gitignore. O repo 
   privado `endurance-os-data` guarda dados reais.

6. **Dois repos**: este (público) tem só código. Dados ficam em 
   `endurance-os-data` (privado), apontado por variável `ATHLETE_DATA_DIR` 
   no .env.

7. **Sempre demonstrável**: `scripts/generate_synthetic_data.py` gera 6 meses 
   de dados fictícios. Qualquer um clona e roda tudo.

8. **Pensar como product builder, não só como engenheiro**: toda feature 
   responde a dor concreta. Documentar dor, hipótese e aprendizado em 
   `PRODUCT_NOTES.md`. Iterar baseado em uso real, não em achismo.

9. **Claude Code é a ferramenta primária**: todo trabalho de código acontece 
   no Claude Code, com este arquivo carregado. Conversas no chat web 
   (claude.ai) são pra planejamento, brainstorm de produto e atualização do 
   `PRODUCT_NOTES.md`. Quando o usuário menciona "vamos codar" ou abre um 
   problema técnico, ele está no Claude Code, não em outro lugar.

## Estrutura do projeto

```
endurance-os/
├── README.md
├── CLAUDE.md
├── PRODUCT_NOTES.md
├── pyproject.toml
├── .gitignore
├── .env.example
├── config/
│   └── athlete_profile.example.yaml
├── src/
│   ├── ingestion/
│   │   ├── strava_oauth.py
│   │   ├── strava_client.py
│   │   ├── strava_sync.py
│   │   └── apple_health.py
│   ├── db/
│   │   ├── schema.sql
│   │   ├── views.sql
│   │   ├── queries/
│   │   └── connection.py
│   ├── metrics/
│   │   ├── training_load.py
│   │   ├── cardiac.py
│   │   └── zones.py
│   ├── reports/
│   │   ├── weekly.py
│   │   └── templates/
│   ├── dashboard/
│   │   └── app.py
│   └── coach/
│       ├── prompts/
│       └── weekly_review.py
├── scripts/
│   ├── generate_synthetic_data.py
│   └── sync_all.py
├── tests/
└── docs/
    ├── architecture.md
    ├── data_model.md
    ├── metrics_explained.md
    └── screenshots/
```

## Stack

- Python 3.11+ (Windows)
- `uv` pra dependências
- `requests` (cliente HTTP próprio, sem `stravalib`)
- SQLite via `sqlite3` nativo, sem ORM
- pandas, Streamlit, plotly, Jinja2
- SDK `anthropic`

## Comandos comuns

```bash
# Setup inicial
uv sync

# Sincronizar Strava
python -m src.ingestion.strava_sync

# Processar Apple Health export
python -m src.ingestion.apple_health --input ~/Downloads/export.xml

# Gerar relatório semanal
python -m src.reports.weekly

# Dashboard
streamlit run src/dashboard/app.py

# Treinador IA
python -m src.coach.weekly_review

# Dados sintéticos
python scripts/generate_synthetic_data.py
```

## Convenções

- Nomes em inglês no código, comentários em português quando útil
- Type hints em todas as funções públicas
- Docstrings estilo Google em funções de métrica (incluir fórmula e referência)
- Variáveis de ambiente em UPPER_SNAKE
- Datas sempre em UTC no banco, convertidas pra TZ local só na exibição
- SQL em arquivos `.sql` separados, não strings embutidas
- Views analíticas pré-computam o que o dashboard consome

## Como Claude Code deve me ajudar

- **Conceitos novos**: OAuth, exponential backoff, window functions em SQL, 
  métricas fisiológicas, prompt engineering — com analogias e exemplos
- **Modelagem de dados**: revisar schemas, sugerir índices, identificar 
  problemas de normalização, propor views
- **Refatorações pequenas** quando algo ficar feio
- **Testes** quando eu fizer função nova
- **Revisão** de mudanças grandes
- **Pensar como product builder**: antes de construir feature nova, perguntar 
  "que dor isso resolve, que hipótese isso testa, como vou saber se funcionou, 
  existe versão mais simples"
- **NÃO fazer plumbing pronto** que eu deveria implementar como aprendizado 
  (OAuth, retry, schema SQL) — me guiar a fazer, não fazer por mim

## Estado atual

[atualizar a cada sessão]

Semana: 1
Foco atual: Setup inicial — repos criados, Git configurado
Hipótese de produto testada nesta fase: "Visão integrada Strava + Apple Health 
muda como entendo meu treino"
Pendências: Strava developer portal, instalar uv, criar estrutura de pastas

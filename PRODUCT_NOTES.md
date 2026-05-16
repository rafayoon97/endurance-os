# Product Notes — endurance-os

Documento vivo de hipóteses, decisões de produto e aprendizados. Atualizado 
ao longo do desenvolvimento. É o material mais importante pro portfólio: 
mostra raciocínio de AI Product Builder, não só execução técnica.

---

## Dor original

Não tenho visão integrada do meu treino. Strava mostra atividades soltas, 
Apple Health mostra saúde solta, nada conversa. Treino corrida e tênis sem 
saber se estou em overtraining, se a carga subiu demais, se vou ter 
desempenho ou lesão.

Apps de mercado atendem parcialmente:
- **TrainingPeaks**: foca corrida, caro, complexo demais pra amador
- **Garmin Connect**: exige ecossistema próprio
- **Whoop**: caro, recovery-only, não é planejamento de treino
- **Strava Premium**: insights superficiais, sem prescrição
- **Coach humano**: caro, não escala, demora pra ajustar

Gap percebido: jogador amador multi-esporte com dados próprios, sem 
ferramenta que entenda a carga combinada e dê recomendação personalizada 
sob demanda.

---

## Hipóteses de produto

### H1: Dashboard pessoal muda comportamento de treino
Ver dados estruturados toda segunda muda decisão de treino da semana?
- **Como validar**: comparar decisões antes/depois do dashboard por 4 semanas
- **Status**: ⬜ pendente — validar após semana 11

### H2: Treinador IA com dados estruturados supera coach genérico
LLM com dados próprios produz recomendação melhor que app de mercado pra 
mesma situação?
- **Como validar**: comparar recomendações da IA com sugestão de app genérico 
  em 5+ semanas consecutivas
- **Status**: ⬜ pendente — validar após semana 14

### H3: Carga unificada multi-esporte é diferencial real
CTL/ATL considerando corrida + tênis produz insight que nenhuma ferramenta 
atual entrega?
- **Como validar**: identificar 1+ decisão tomada com base na visão combinada 
  que ferramentas tradicionais não permitiriam
- **Status**: ⬜ pendente — validar após semana 17

### H4: Modelagem de dados é o moat, não o LLM
A qualidade do treinador IA é mais função da qualidade dos dados estruturados 
(schema, views, métricas derivadas) do que do prompt em si?
- **Como validar**: comparar output do treinador com dados crus vs com views 
  pré-computadas e métricas derivadas
- **Status**: ⬜ pendente — validar após semana 14

---

## Aprendizados por fase

### Bloco 1 — Fundação (semanas 1-4)
[preencher ao longo das semanas]

### Bloco 2 — Análise (semanas 5-8)
[preencher]

### Bloco 3 — Visualização (semanas 9-12)
[preencher]

### Bloco 4 — IA (semanas 13-15)
[preencher]

### Bloco 5 — Convergência tênis (semanas 16-17)
[preencher]

---

## Decisões de produto importantes

[registrar quando tomar uma decisão não-óbvia — ex: "decidi não mostrar 
recomendação numérica de pace, só zonas, porque estava virando prescriptive 
demais sem base suficiente"]

---

## Retrospectiva final

[escrever na semana 18, antes do post de LinkedIn]

- O que funcionou bem
- O que não funcionou
- O que mudaria se começasse de novo
- Próximos passos — produto ou mercado

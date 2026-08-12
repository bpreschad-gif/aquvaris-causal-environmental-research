# Associação contemporânea entre SO₂ e material particulado (PM10) em estação de foco industrial: um estudo em Cubatão-Vila Parisi, Brasil (2021–2022)

**Bruna Preschadt de Oliveira**
Aquvaris AI

**Versão 1.1** — rascunho científico. Números verificados contra o notebook de análise (checklist de auditoria de 11 itens, todos conferidos); referências verificadas individualmente. Revisão 1.1: co-emissão reportada como hipótese interpretativa; métodos de refutação nomeados; R² do modelo final corrigido e interpretado; limitação de agregação da fonte explicitada.

---

## Resumo

Sistemas de qualidade do ar tipicamente monitoram e, cada vez mais, preveem concentrações de poluentes, mas raramente **atribuem** uma variação a uma fonte específica separando-a de confundidores. Este estudo examina a relação entre SO₂ (marcador de queima industrial) e PM10 (material particulado) na estação Cubatão-Vila Parisi, caracterizada pela CETESB como de foco industrial, com atenção explícita à estrutura temporal dos dados antes de qualquer interpretação causal. Sobre 605 dias (2021–2022), estimou-se por regressão linear, com erros-padrão robustos a heterocedasticidade e autocorrelação (HAC/Newey-West), uma associação contemporânea de 0,4481 µg/m³ de PM10 por µg/m³ de SO₂ (IC 95%: 0,1756–0,7207; p = 1,27×10⁻³; R² ajustado = 0,535). A associação é estável ao controle sazonal e à escolha do parâmetro de defasagem do HAC; não há efeito defasado detectável em escala diária. O padrão é **consistente com co-emissão por fonte industrial comum**, embora os dados não permitam isolar esse mecanismo de explicações alternativas. A contribuição é dupla: uma associação quantificada e auditável em um polo industrial brasileiro, e um protocolo reprodutível que separa associação de estrutura temporal antes de concluir.

---

## 1. Pergunta científica

Quando um poluente atmosférico varia, quanto dessa variação está associado à assinatura de uma fonte específica — e essa associação sobrevive ao controle de meteorologia, sazonalidade, tendência e outras fontes? O estudo trata dessa pergunta para o par SO₂–PM10, com ênfase em **investigar a natureza temporal do sinal** antes de qualquer alegação causal, em vez de reportar um único coeficiente ajustado.

## 2. Contexto: Cubatão-Vila Parisi

Cubatão (SP) é referência histórica da poluição industrial brasileira; na década de 1980 as indústrias da região chegaram a lançar cerca de mil toneladas de poluentes atmosféricos por dia, revertidas parcialmente por um programa de controle a partir de 1983 (CETESB). A estação Cubatão-Vila Parisi é caracterizada pela própria CETESB como de **foco industrial**, sem equivalente entre as demais estações de monitoramento do estado de São Paulo. O estudo não extrapola para o período crítico das décadas de 1980–90: os dados analisados são de 2021–2022, período de operação regulada.

## 3. Dados

- **Poluentes:** SO₂, PM10, NO₂ — médias diárias da estação Cubatão-V.Parisi, obtidas via API do OpenAQ, que registra a **CETESB** (Companhia Ambiental do Estado de São Paulo) como provedora dos dados (provider ID 220). A agregação de resolução horária para diária é realizada pela fonte.
- **Meteorologia:** temperatura, precipitação, vento, umidade e pressão — reanálise histórica diária (Open-Meteo).
- **Período:** 12/01/2021 a 31/12/2022. **N = 605 dias** completos após limpeza. As séries diárias dos três poluentes ao longo do período são apresentadas na Figura 1.
- **Qualidade / auditoria:** valores ≤ 0 tratados como ausentes; um registro por dia (sem agregação adicional nossa); merge com meteorologia 1-para-1 (sem duplicação); 16 lacunas curtas na série bruta. Defasagens temporais construídas por data-calendário (575 pares consecutivos válidos), não por posição de linha.

## 4. Desenho causal e estratégia de identificação

- **Relação de interesse:** SO₂ → PM10.
- **Confundidores medidos:** NO₂; temperatura, precipitação, vento, umidade e pressão; sazonalidade (indicadores de mês) e tendência temporal linear.
- **Tratamento do NO₂:** a correlação SO₂–NO₂ observada foi baixa (0,193), sugerindo fontes majoritariamente distintas; o NO₂ é incluído como confundidor.
- **Ressalva de identificação:** uma relação *contemporânea* entre SO₂ e PM10 é compatível tanto com conversão química (SO₂ oxidado a sulfato, formando PM secundário) quanto com co-emissão por fonte comum (uma fonte industrial emitindo SO₂ e PM primário simultaneamente). Ambos os mecanismos são fisicamente documentados para material particulado (Seinfeld & Pandis, 2016) e reconhecidos pela CETESB para a própria Vila Parisi. **A estrutura contemporânea não distingue essas alternativas.** Consequentemente, o estimando é reportado como **associação ajustada**, não como efeito causal de fonte.

## 5. Estimativa

Regressão linear de PM10 sobre SO₂ com o conjunto completo de controles (clima + NO₂ + mês + tendência). Dada a natureza de série temporal dos resíduos (ver §7), a inferência é conduzida com erros-padrão HAC (Newey & West, 1987).

**Associação contemporânea estimada: 0,4481 µg/m³ de PM10 por µg/m³ de SO₂**
(IC 95% [HAC, 7 defasagens]: 0,1756–0,7207; p = 1,27×10⁻³; N = 605).

A relação bruta (sem controles) é apresentada na Figura 2; sua inclinação (~1,28) é cerca de 2,8 vezes o efeito ajustado, ilustrando a magnitude do confundimento removido pelos controles.

O modelo final explica cerca de 55% da variância diária do PM10 (R² = 0,549; R² ajustado = 0,535). Os ~45% restantes correspondem a fatores não incluídos no modelo — outras fontes, transporte atmosférico, variabilidade não capturada pelas covariáveis —, o que reforça a leitura do resultado como associação parcial, não como determinação completa do PM10 pelo SO₂.

Para referência, o valor de comparação por convergent cross mapping em Jakarta situou a causalidade SO₂→PM2.5 em 0,68 (Aerosol and Air Quality Research, 2023) — ordem de magnitude compatível, em contexto e método distintos.

## 6. Estrutura temporal do sinal

Três especificações temporais foram estimadas (SO₂ de t+1, t e t−1 sobre PM10 de t), com e sem controle de sazonalidade (Figura 3):

| Especificação | β (sem sazonalidade) | β (com sazonalidade) |
|---|---|---|
| t+1 → t (placebo temporal) | 0,2144 | 0,2071 |
| t → t (contemporâneo) | 0,4704 | 0,4481 |
| t−1 → t (defasado 1 dia) | 0,0937 (n.s.) | 0,0850 (n.s.) |

**Leitura:**
- O efeito contemporâneo é **estável ao controle sazonal** (0,4704 → 0,4481): não é artefato de sazonalidade.
- A associação defasada de um dia é **nula** (não significativa): sem evidência de mecanismo de conversão lenta detectável em escala diária — compatível com processo contemporâneo (co-emissão).
- O placebo t+1 residual (~0,21) não é eliminado pelo controle sazonal e é interpretado como consequência da **autocorrelação do PM10** (0,58, ver §7), não como confundimento sazonal. Sua magnitude é cerca de metade do efeito contemporâneo, indicando sinal contemporâneo além da persistência.
- A inclusão vs. exclusão de NO₂ altera pouco o efeito (0,4481 vs. 0,4895): NO₂ atua como confundidor de efeito modesto, não como co-emissor dominante.

**Testes de refutação (especificação de referência).** Testes de refutação por inferência causal — causa comum aleatória, placebo por permutação do tratamento e subamostragem (80%) — foram conduzidos sobre a especificação de referência (efeito 0,4704, sem controle sazonal). O efeito manteve-se estável sob adição de causa comum aleatória (0,4704 → 0,4704) e sob subamostragem (0,4704 → 0,4859), e caiu para ~0 sob tratamento-placebo (0,4704 → 0,0079), como esperado. A especificação final adiciona controle de sazonalidade e tendência — que altera o efeito em menos de 5% (0,4704 → 0,4481) — e adota inferência HAC, que refina o intervalo de confiança sem alterar a estimativa pontual. A estrutura avaliada pelos refutadores (presença de efeito, colapso sob placebo, estabilidade sob subamostragem) é, portanto, preservada na especificação final.

## 7. Inferência robusta

Diagnóstico dos resíduos do modelo contemporâneo indicou autocorrelação (Durbin-Watson = 1,271; Ljung-Box p ≪ 0,001 em defasagens 1 e 7) e heterocedasticidade (Breusch-Pagan p ≈ 1×10⁻⁵). Sob essas condições, os erros-padrão convencionais subestimam a incerteza (Newey & West, 1987); a estimativa pontual do coeficiente não é afetada.

Adotou-se HAC/Newey-West como inferência principal. A sensibilidade à escolha do número máximo de defasagens foi avaliada comparando 7 defasagens (janela de curto prazo definida a priori) e 8 (especificação alternativa), mantidos constantes os demais parâmetros do estimador:

| HAC (defasagens) | IC 95% | p |
|---|---|---|
| 7 | 0,1756–0,7207 | 1,27×10⁻³ |
| 8 | 0,1714–0,7248 | 1,50×10⁻³ |

A variação nos limites do IC entre 7 e 8 defasagens foi inferior a 0,005 µg/m³ e a significância permaneceu na ordem de 10⁻³: a inferência **não depende materialmente** dessa escolha. O IC robusto é cerca de 30% mais largo que o convencional (0,545 vs. 0,419), refletindo a incerteza real da série.

## 8. Protocolo metodológico

O estudo instancia um protocolo reprodutível para análise de associações ambientais em séries temporais, que constitui uma contribuição independente do resultado específico:

> **detectar → controlar → testar temporalidade → checar robustez → declarar limites → (só então) atribuir**

Concretamente: (1) detectar a associação bruta; (2) controlar confundidores medidos (clima, sazonalidade, tendência, outras fontes); (3) testar a estrutura temporal (placebo t+1, defasada t−1) para distinguir sinal contemporâneo de estrutura compartilhada; (4) checar robustez (inferência HAC, sensibilidade de defasagens, com/sem confundidor); (5) declarar explicitamente os limites de identificação; (6) reservar a atribuição causal para quando o desenho a sustentar. O protocolo desloca a pergunta de "existe efeito?" para "de que natureza é o sinal?".

## 9. Limitações

- A estrutura contemporânea não distingue conversão química de co-emissão.
- A resolução diária pode mascarar dinâmica de sub-dia (mecanismos químicos operam em horas). Além disso, a agregação de resolução horária para diária é realizada pela fonte (OpenAQ/CETESB) e não é auditável pelos autores: não temos acesso ao critério de agregação (média sobre quais horas, exigência mínima de cobertura), o que constitui uma fonte de incerteza não quantificada.
- Confundidores não observados podem persistir; a estimativa é condicional ao conjunto de controles adotado.
- Estação única; o método de agregação horária→diária da fonte não é controlado pelos autores.
- Estimador linear; formas não-lineares não foram avaliadas nesta versão.
- O NO₂ como confundidor pressupõe fontes distintas; a baixa correlação observada apoia, mas não prova, essa premissa.

## 10. Conclusão

Encontrou-se uma **associação contemporânea robusta** entre SO₂ e PM10 na estação industrial de Vila Parisi (0,4481 µg/m³ por µg/m³; IC 95% robusto 0,1756–0,7207), estável ao controle de meteorologia, sazonalidade, tendência e NO₂, à escolha do parâmetro de inferência, e aos métodos de refutação aplicados (tratamento-placebo, subamostragem e adição de causa comum aleatória). A ausência de efeito defasado e a estabilidade contemporânea são **consistentes com co-emissão por fonte industrial comum, embora os dados não permitam isolar esse mecanismo de explicações alternativas** (por exemplo, conversão química rápida ou uma fonte latente comum não medida). O estudo não sustenta, com os dados disponíveis, uma afirmação de efeito causal direto SO₂→PM10; sustenta uma associação ajustada com interpretação física plausível e limites explicitamente declarados.

## 11. Trabalho futuro

- Dados horários, para investigar dinâmica de sub-dia e distinguir conversão de co-emissão.
- Replicação em Cubatão-Vale do Mogi e em outros polos industriais.
- Estimadores não-lineares e métodos de séries temporais causais (ex.: modelos de defasagens distribuídas; convergent cross mapping).

---

## Reprodutibilidade

Código, dados e documentação: `github.com/bpreschad-gif/aquvaris-causal-environmental-research`

## Figuras

- **Figura 1** — Séries temporais diárias de SO₂, PM10 e NO₂ em Cubatão-Vila Parisi (2021–2022). (`results/figures/fig1_series.png`)
- **Figura 2** — Relação bruta SO₂–PM10 com reta de ajuste (inclinação ≈ 1,28). (`results/figures/fig2_dispersao.png`)
- **Figura 3** — Efeito ajustado sobre PM10 nas três especificações temporais (t+1 placebo, t contemporâneo, t−1 defasado), com intervalos de confiança de 95%. (`results/figures/fig3_temporal.png`)

## Referências

- Nardocci, A. C.; Freitas, C. U.; Ponce de Leon, A. C. M.; Junger, W. L.; Gouveia, N. C. (2013). Poluição do ar e doenças respiratórias e cardiovasculares: estudo de séries temporais em Cubatão, São Paulo, Brasil. *Cadernos de Saúde Pública*, 29(9), 1867–1876.
- Newey, W. K.; West, K. D. (1987). A Simple, Positive Semi-Definite, Heteroskedasticity and Autocorrelation Consistent Covariance Matrix. *Econometrica*, 55(3), 703–708.
- Seinfeld, J. H.; Pandis, S. N. (2016). *Atmospheric Chemistry and Physics: From Air Pollution to Climate Change* (3rd ed.). Wiley.
- Tec, M.; Scott, J. G.; Zigler, C. M. (2023). Weather2vec: Representation Learning for Causal Inference with Non-Local Confounding in Air Pollution and Climate Studies. *arXiv:2209.12316*.
- [Jakarta / CCM] Causality Analysis of Air Quality and Meteorological Parameters for PM2.5 Characteristics Determination: Evidence from Jakarta. *Aerosol and Air Quality Research* (2023).
- CETESB — Companhia Ambiental do Estado de São Paulo. Rede automática de monitoramento da qualidade do ar; caracterização da estação Cubatão-Vila Parisi; relatórios de qualidade do ar.

*Referências a expandir na versão de submissão: literatura adicional de inferência causal em qualidade do ar e de co-emissão SO₂/PM em fontes industriais.*

# Associação contemporânea entre SO₂ e material particulado (PM10) em estações de foco industrial: um estudo com replicação em Cubatão, Brasil (2021–2022)

**Bruna Preschadt de Oliveira**
Aquvaris AI

**Versão 1.3** — rascunho científico. Números verificados contra o notebook de análise (checklist de auditoria de 11 itens, todos conferidos) e reauditados após a replicação; referências verificadas individualmente. Revisão 1.3: revisão de redação para prosa científica corrida; resumo reescrito pela autora; conteúdo, números e ressalvas metodológicas preservados.

---

## Resumo

Sistemas de monitoramento da qualidade do ar permitem acompanhar as concentrações de diferentes poluentes, mas a interpretação conjunta dessas séries é limitada pela presença de fatores meteorológicos, sazonais e outras fontes de emissão. Este estudo examina a associação entre SO₂, indicador de emissões associadas à combustão e a processos industriais, e PM10 em estações de foco industrial de Cubatão (SP), incorporando a estrutura temporal dos dados antes de qualquer interpretação causal. Na estação Cubatão-Vila Parisi, ao longo de 605 dias entre 2021 e 2022, uma regressão linear com erros-padrão robustos à heterocedasticidade e autocorrelação (HAC/Newey-West) estimou uma associação contemporânea de 0,4481 µg/m³ de PM10 por µg/m³ de SO₂ (IC 95%: 0,1756–0,7207; p = 1,27×10⁻³; R² ajustado = 0,535). A estimativa permaneceu semelhante após o controle de sazonalidade e a alteração do número de defasagens do estimador HAC, enquanto não foi detectada associação estatisticamente significativa entre SO₂ de um dia anterior e PM10 do dia seguinte. A aplicação do mesmo procedimento à estação Cubatão-Vale do Mogi, com 597 dias, produziu associação positiva de maior magnitude (0,8461; IC 95%: 0,5396–1,1525; p = 6,24×10⁻⁸). Embora a diferença entre as estimativas seja sugestiva, o teste formal de heterogeneidade não indicou diferença estatisticamente significativa entre as estações (p = 0,11). O padrão observado é compatível com co-emissão por fontes industriais comuns, mas os dados não permitem distinguir esse mecanismo de outras explicações, como processos atmosféricos de formação de partículas. O estudo apresenta uma associação quantitativamente estimada e replicada em duas estações industriais de Cubatão, além de um procedimento de análise que incorpora estrutura temporal e testes de robustez antes da interpretação ambiental.

---

## 1. Pergunta científica

Quando a concentração de um poluente atmosférico varia, quanto dessa variação pode ser associado à assinatura de uma fonte específica, e essa associação persiste após o controle de meteorologia, sazonalidade, tendência e outras fontes? O estudo trata dessa questão para o par SO₂–PM10, priorizando a investigação da natureza temporal do sinal antes de qualquer alegação causal, em lugar de reportar um único coeficiente ajustado.

## 2. Contexto: Cubatão-Vila Parisi

Cubatão (SP) é uma referência histórica da poluição industrial brasileira. Na década de 1980, as indústrias da região chegaram a lançar cerca de mil toneladas de poluentes atmosféricos por dia, quadro parcialmente revertido por um programa de controle iniciado em 1983 (CETESB). A estação Cubatão-Vila Parisi é caracterizada pela própria CETESB como de foco industrial, sem equivalente entre as demais estações de monitoramento do estado de São Paulo. Este estudo não extrapola para o período crítico das décadas de 1980–90; os dados analisados correspondem a 2021–2022, período de operação regulada.

## 3. Dados

- Poluentes: SO₂, PM10 e NO₂, em médias diárias da estação Cubatão-V.Parisi, obtidas via API do OpenAQ, que registra a CETESB (Companhia Ambiental do Estado de São Paulo) como provedora dos dados (provider ID 220). A agregação de resolução horária para diária é realizada pela fonte.
- Meteorologia: temperatura, precipitação, vento, umidade e pressão, de reanálise histórica diária (Open-Meteo).
- Período: de 12/01/2021 a 31/12/2022, totalizando 605 dias completos após a limpeza. As séries diárias dos três poluentes ao longo do período são apresentadas na Figura 1.
- Qualidade e auditoria: valores ≤ 0 foram tratados como ausentes; há um registro por dia (sem agregação adicional de nossa parte); o merge com a meteorologia é 1-para-1 (sem duplicação); a série bruta contém 16 lacunas curtas. As defasagens temporais foram construídas por data-calendário (575 pares consecutivos válidos), não por posição de linha.

## 4. Desenho causal e estratégia de identificação

- Relação de interesse: SO₂ → PM10.
- Confundidores medidos: NO₂; temperatura, precipitação, vento, umidade e pressão; sazonalidade (indicadores de mês) e tendência temporal linear.
- Tratamento do NO₂: a correlação SO₂–NO₂ observada foi baixa (0,193), o que sugere fontes majoritariamente distintas; por isso o NO₂ entra como confundidor.
- Ressalva de identificação: uma relação contemporânea entre SO₂ e PM10 é compatível tanto com conversão química (SO₂ oxidado a sulfato, formando PM secundário) quanto com co-emissão por fonte comum (uma fonte industrial que emite SO₂ e PM primário simultaneamente). Ambos os mecanismos estão documentados para material particulado (Seinfeld & Pandis, 2016) e são reconhecidos pela CETESB para a própria Vila Parisi. A estrutura contemporânea não distingue essas alternativas. Em consequência, o estimando é reportado como associação ajustada, não como efeito causal de fonte.

## 5. Estimativa

Estimou-se uma regressão linear de PM10 sobre SO₂ com o conjunto completo de controles (meteorologia, NO₂, mês e tendência). Dada a natureza de série temporal dos resíduos (ver §7), a inferência foi conduzida com erros-padrão HAC (Newey & West, 1987).

A associação contemporânea estimada foi de 0,4481 µg/m³ de PM10 por µg/m³ de SO₂ (IC 95% [HAC, 7 defasagens]: 0,1756–0,7207; p = 1,27×10⁻³; N = 605).

A relação bruta, sem controles, é apresentada na Figura 2; sua inclinação (aproximadamente 1,28) corresponde a cerca de 2,8 vezes o efeito ajustado, o que ilustra a magnitude do confundimento removido pelos controles.

O modelo final explica cerca de 55% da variância diária do PM10 (R² = 0,549; R² ajustado = 0,535). Os aproximadamente 45% restantes correspondem a fatores fora do modelo — outras fontes, transporte atmosférico e variabilidade não capturada pelas covariáveis —, o que reforça a leitura do resultado como associação parcial, e não como determinação completa do PM10 pelo SO₂.

Como referência externa, uma análise por convergent cross mapping em Jakarta situou a causalidade SO₂→PM2.5 em 0,68 (Aerosol and Air Quality Research, 2023), ordem de magnitude compatível, ainda que em contexto e método distintos.

## 6. Estrutura temporal do sinal

Três especificações temporais foram estimadas (SO₂ de t+1, t e t−1 sobre PM10 de t), com e sem controle de sazonalidade (Figura 3):

| Especificação | β (sem sazonalidade) | β (com sazonalidade) |
|---|---|---|
| t+1 → t (placebo temporal) | 0,2144 | 0,2071 |
| t → t (contemporâneo) | 0,4704 | 0,4481 |
| t−1 → t (defasado 1 dia) | 0,0937 (n.s.) | 0,0850 (n.s.) |

A leitura dessas estimativas é a seguinte. O efeito contemporâneo permanece estável ao controle sazonal (de 0,4704 para 0,4481), o que afasta a hipótese de artefato de sazonalidade. A associação defasada de um dia é nula (não significativa), sem evidência de um mecanismo de conversão lenta detectável em escala diária, o que é compatível com um processo contemporâneo, como a co-emissão. O placebo temporal em t+1 permanece em torno de 0,21 mesmo após o controle sazonal; sua persistência é atribuída à autocorrelação do PM10 (0,58, ver §7), e não a confundimento sazonal — sua magnitude, cerca de metade do efeito contemporâneo, indica sinal contemporâneo além da mera persistência. Por fim, incluir ou excluir o NO₂ altera pouco a estimativa (0,4481 contra 0,4895), o que posiciona o NO₂ como confundidor de efeito modesto, não como co-emissor dominante.

Testes de refutação por inferência causal — adição de causa comum aleatória, placebo por permutação do tratamento e subamostragem a 80% — foram conduzidos sobre a especificação de referência (efeito de 0,4704, sem controle sazonal). O efeito manteve-se estável sob a causa comum aleatória (0,4704 para 0,4704) e sob a subamostragem (0,4704 para 0,4859), e caiu para próximo de zero sob o tratamento-placebo (0,4704 para 0,0079), como esperado. A especificação final acrescenta controle de sazonalidade e tendência — que alteram o efeito em menos de 5% (0,4704 para 0,4481) — e adota a inferência HAC, que refina o intervalo de confiança sem mover a estimativa pontual. A estrutura avaliada pelos refutadores, a saber, presença de efeito, colapso sob placebo e estabilidade sob subamostragem, é assim preservada na especificação final.

## 7. Inferência robusta

Diagnóstico dos resíduos do modelo contemporâneo indicou autocorrelação (Durbin-Watson = 1,271; Ljung-Box p ≪ 0,001 em defasagens 1 e 7) e heterocedasticidade (Breusch-Pagan p ≈ 1×10⁻⁵). Sob essas condições, os erros-padrão convencionais subestimam a incerteza (Newey & West, 1987); a estimativa pontual do coeficiente não é afetada.

Adotou-se HAC/Newey-West como inferência principal. A sensibilidade à escolha do número máximo de defasagens foi avaliada comparando 7 defasagens (janela de curto prazo definida a priori) e 8 (especificação alternativa), mantidos constantes os demais parâmetros do estimador:

| HAC (defasagens) | IC 95% | p |
|---|---|---|
| 7 | 0,1756–0,7207 | 1,27×10⁻³ |
| 8 | 0,1714–0,7248 | 1,50×10⁻³ |

A variação nos limites do intervalo de confiança entre 7 e 8 defasagens foi inferior a 0,005 µg/m³, e a significância permaneceu na ordem de 10⁻³: a inferência não depende materialmente dessa escolha. O intervalo robusto é cerca de 30% mais largo que o convencional (0,545 contra 0,419), o que reflete a incerteza real da série.

## 8. Replicação em segunda estação

Para avaliar se a associação é específica de uma estação ou reflete um padrão da zona industrial, o pipeline completo — mesma especificação, mesmos controles e mesma inferência HAC-7 — foi aplicado à estação Cubatão-Vale do Mogi, o outro polo industrial monitorado na região (597 dias completos).

| Estação | β (SO₂→PM10) | IC 95% (HAC-7) | p | N |
|---|---|---|---|---|
| Cubatão-Vila Parisi | 0,4481 | 0,1756–0,7207 | 1,27×10⁻³ | 605 |
| Cubatão-Vale do Mogi | 0,8461 | 0,5396–1,1525 | 6,24×10⁻⁸ | 597 |

A associação replica-se: em ambas as estações o efeito é positivo, robusto e altamente significativo. Isso indica que o padrão SO₂–PM10 não é artefato de uma estação isolada.

O coeficiente pontual é maior em Vale do Mogi (0,85) que em Vila Parisi (0,45). Para avaliar se essa diferença é estatisticamente distinguível de variação amostral, estimou-se um modelo combinado das duas estações com interação completa (cada estação com seus próprios controles), extraindo o termo de interação SO₂ × estação com inferência HAC-7. A verificação de consistência confirmou que o modelo combinado reproduz os coeficientes dos modelos separados (0,445 e 0,805). A diferença estimada foi de 0,3602 (IC 95%: −0,0838–0,8042; p = 0,11): sugestiva, mas não estatisticamente significativa ao nível convencional. Os dados são, portanto, insuficientes para afirmar heterogeneidade real entre as estações — a diferença de magnitude pode refletir variação amostral, e distinguir as duas hipóteses exigiria mais estações ou séries mais longas. A ausência de significância não implica igualdade dos coeficientes; implica insuficiência de dados para decidir.

## 9. Protocolo metodológico

O estudo instancia um protocolo reprodutível para análise de associações ambientais em séries temporais, que constitui uma contribuição independente do resultado específico:

> detectar → controlar → testar temporalidade → checar robustez → declarar limites → (só então) atribuir

Concretamente: (1) detectar a associação bruta; (2) controlar confundidores medidos (clima, sazonalidade, tendência, outras fontes); (3) testar a estrutura temporal (placebo t+1, defasada t−1) para distinguir sinal contemporâneo de estrutura compartilhada; (4) checar robustez (inferência HAC, sensibilidade de defasagens, com/sem confundidor); (5) declarar explicitamente os limites de identificação; (6) reservar a atribuição causal para quando o desenho a sustentar. O protocolo desloca a pergunta de "existe efeito?" para "de que natureza é o sinal?".

## 10. Limitações

- A estrutura contemporânea não distingue conversão química de co-emissão.
- A resolução diária pode mascarar dinâmica de sub-dia (mecanismos químicos operam em horas). Além disso, a agregação de resolução horária para diária é realizada pela fonte (OpenAQ/CETESB) e não é auditável pelos autores: não temos acesso ao critério de agregação (média sobre quais horas, exigência mínima de cobertura), o que constitui uma fonte de incerteza não quantificada.
- Confundidores não observados podem persistir; a estimativa é condicional ao conjunto de controles adotado.
- Duas estações da mesma região (Cubatão); a generalização para outras regiões e matrizes industriais permanece a testar. A diferença de magnitude entre as estações é sugestiva mas não conclusiva (§8).
- Estimador linear; formas não-lineares não foram avaliadas nesta versão.
- O NO₂ como confundidor pressupõe fontes distintas; a baixa correlação observada apoia, mas não prova, essa premissa.

## 11. Conclusão

Este estudo encontrou uma associação contemporânea robusta entre SO₂ e PM10 em estação industrial de Cubatão (Vila Parisi: 0,4481 µg/m³ por µg/m³; IC 95% robusto: 0,1756–0,7207). A estimativa manteve-se estável ao controle de meteorologia, sazonalidade, tendência e NO₂, à escolha do parâmetro de inferência e aos métodos de refutação aplicados (tratamento-placebo, subamostragem e adição de causa comum aleatória). A associação replicou-se em uma segunda estação industrial (Vale do Mogi: 0,8461; p = 6,24×10⁻⁸), o que indica um padrão não restrito a um único ponto de monitoramento; a diferença de magnitude entre as estações é sugestiva, mas não atinge significância estatística. A ausência de efeito defasado e a estabilidade contemporânea são consistentes com co-emissão por uma fonte industrial comum, ainda que os dados não permitam isolar esse mecanismo de explicações alternativas, como a conversão química rápida ou a presença de uma fonte latente comum não medida. Com os dados disponíveis, o estudo não sustenta uma afirmação de efeito causal direto de SO₂ sobre PM10; sustenta, sim, uma associação ajustada e replicada, com interpretação física plausível e limites explicitamente declarados.

## 12. Trabalho futuro

- Dados horários, para investigar dinâmica de sub-dia e distinguir conversão de co-emissão.
- Replicação em polos industriais de outras regiões e matrizes produtivas (a heterogeneidade sugerida entre Vila Parisi e Vale do Mogi motiva ampliar o número de estações).
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

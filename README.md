# Aquvaris — Causal Environmental Research

**Atribuição causal de fontes em séries temporais ambientais.**

Primeiro estudo: efeito do SO₂ sobre material particulado (PM10) em Cubatão-Vila Parisi, Brasil (2021–2022).

Este é um repositório de **pesquisa**, não de produto. O objetivo é permitir que um pesquisador reproduza mentalmente o experimento antes mesmo de executar o código, seguindo a ordem: pergunta → hipótese → dados → DAG → identificação → estimador → refutação → resultado → limitações → reprodução.

---

## 1. Pergunta

Quando um poluente atmosférico varia, quanto dessa variação pode ser atribuído *causalmente* a uma fonte específica — e não a confundidores como meteorologia e sazonalidade?

## 2. Hipótese

Em Vila Parisi (Cubatão), zona de emissão industrial histórica, variações de SO₂ (marcador de queima industrial) exercem efeito causal positivo sobre PM10 (material particulado), mesmo após controlar por meteorologia e por NO₂ (marcador de tráfego).

## 3. Dados

- **Poluentes:** SO₂, PM10, NO₂ — médias diárias, estação Cubatão-V.Parisi, via OpenAQ (endpoint `/days`). Período: jan/2021–dez/2022.
- **Meteorologia:** temperatura, precipitação, vento, umidade, pressão — via Open-Meteo (reanálise histórica).
- **Amostra final:** 605 dias completos após limpeza.
- **Tratamento de qualidade:** valores ≤ 0 tratados como ausentes (fisicamente implausíveis em ambiente urbano).

## 4. Estrutura causal (DAG)

- **Tratamento:** SO₂
- **Desfecho:** PM10
- **Confundidores:** NO₂, temperatura, precipitação, vento, umidade, pressão.
- **Justificativa da inclusão de NO₂:** correlação SO₂–NO₂ = 0,193 (baixa), indicando fontes distintas — NO₂ é tratado como confundidor, não como poluente co-emitido pela mesma fonte.

## 5. Identificação e estimativa

- Identificação via critério *backdoor* (ajuste pelos confundidores).
- Estimador: regressão linear.
- **Efeito estimado:** 0,4704 µg/m³ de PM10 por µg/m³ de SO₂ (IC 95%: 0,2594–0,6814; p = 1,41×10⁻⁵; R² = 0,510; N = 605).

O resultado é reportado como uma estimativa causal **sob os pressupostos do modelo adotado**, não como afirmação causal definitiva.

## 6. Refutação

| Teste | Esperado | Efeito original | Novo efeito |
|---|---|---|---|
| Causa comum aleatória | efeito estável | 0,4704 | 0,4704 |
| Placebo (tratamento permutado) | efeito → ~0 | 0,4704 | 0,0079 |
| Subconjunto (80% dos dados) | efeito estável | 0,4704 | 0,4859 |

## 7. Resultado

Sob os pressupostos do modelo, estima-se um efeito causal positivo e estatisticamente significativo do SO₂ sobre o PM10 em Vila Parisi, robusto aos três testes de refutação aplicados.

## 8. Limitações

- Estimativa condicional aos confundidores incluídos; confundidores não observados podem persistir.
- Efeito médio no período; não captura dinâmica de curtíssimo prazo (episódios de poucas horas).
- Um único local. Replicação em andamento (Cubatão-Vale do Mogi).
- Regressão linear como estimador; especificações alternativas serão avaliadas em análise de sensibilidade.

## 9. Reprodução

```bash
pip install -r requirements.txt
# executar os notebooks na ordem 01 → 06
```

---

## Estrutura do repositório

```
aquvaris-causal-environmental-research/
├── README.md
├── LICENSE
├── CITATION.cff
├── docs/
│   ├── manifesto-0.md
│   ├── methodology.md
│   ├── assumptions.md
│   └── limitations.md
├── data/
│   ├── README.md
│   └── metadata/
├── notebooks/
│   ├── 01_data_diagnostics.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   ├── 03_causal_dag.ipynb
│   ├── 04_dowhy_estimation.ipynb
│   ├── 05_refutation_tests.ipynb
│   └── 06_sensitivity_analysis.ipynb
├── src/
│   ├── data/
│   ├── preprocessing/
│   ├── causal/
│   └── visualization/
├── results/
│   ├── tables/
│   ├── figures/
│   └── models/
└── paper/
    ├── figures/
    ├── tables/
    └── manuscript.md
```

---

*Aquvaris AI — iniciativa de pesquisa em atribuição causal ambiental.*

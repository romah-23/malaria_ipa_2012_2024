# Malária na Amazônia Ocidental: Dinâmica Espaço-Temporal e Desigualdades (2012–2024)

## Descrição

Repositório de dados e códigos analíticos do manuscrito:

> **Malária na Amazônia Ocidental: Dinâmica Espaço-Temporal e Desigualdades (2012–2024)**
> Submetido à Revista de Saúde Pública (RSP/USP), 2026.

O estudo analisa a dinâmica espaço-temporal e as desigualdades sociodemográficas da malária nos 151 municípios da Amazônia Ocidental Brasileira (Acre, Amazonas, Rondônia e Roraima) entre 2012 e 2024, com projeção de cenários epidemiológicos para o período 2025–2030.

---

## Autor

**Pedro Omar Batista Pereira**
Bioestatístico | Universidade Federal do Acre (UFAC)
📧 pedro.omar@sou.ufac.br

---

## Conteúdo do repositório

```
M3/
├── 1 - ESPACIAL/          # Outputs do SaTScan™ por categoria (shapefiles .gis)
│   ├── 1 - SEXO/
│   ├── 2 - IDADE/
│   ├── 3 - COR/
│   └── 4 - ESCOLARIDADE/
├── 2 - TEMPORAL/          # Séries temporais de casos e população por categoria
│   ├── 1 - SEXO/
│   ├── 2 - IDADE/
│   ├── 3 - COR/
│   ├── 4 - ESCOLARIDADE/
│   └── Saida_Prais_Projetada/
├── 3 - PROPORCIONAL/      # Dados proporcionais (gestante, espécie, LPI)
└── 4 - DESCRITIVAS/       # Casos e denominadores populacionais por UF

ao_coordenadas.*           # Coordenadas dos municípios (input SaTScan)
ao_fatores_cor.*           # Fatores bifásicos de calibração por cor/raça
ao_fatores_escolaridade.*  # Fatores bifásicos de calibração por escolaridade
ao_pedido_govbr.*          # Protocolo de solicitação via Lei de Acesso à Informação
```

---

## Como reproduzir as análises

### Pré-requisitos

```r
install.packages(c("sf", "tidyverse", "geobr", "ggplot2",
                   "abjutils", "gridExtra", "grid", "prais",
                   "dplyr", "tidyr"))
```

### Execução

```r
source("malaria_ipa_github.R")
```

O script baixa os dados diretamente deste repositório, processa todas as análises e salva os resultados na pasta `resultados_malaria/` no seu diretório de trabalho. Nenhum download manual é necessário.

### Saídas geradas

| Arquivo | Descrição |
|---|---|
| `Painel_SEXO.png` | Mapa de aglomerados espaciais — sexo biológico |
| `Painel_IDADE.png` | Mapa de aglomerados espaciais — faixa etária |
| `Painel_COR.png` | Mapa de aglomerados espaciais — cor/raça |
| `Painel_ESCOLARIDADE.png` | Mapa de aglomerados espaciais — escolaridade |
| `Tabela_Prais_Regional.csv` | VPA, IC95% e tendência por subgrupo (Prais-Winsten) |
| `Tabela_Projecao_2030.csv` | Projeção do IPA 2025–2030 por subgrupo |
| `Grafico_*_2030.png` | Gráficos temporais com histórico e projeção |

---

## Detecção de aglomerados espaciais (SaTScan™)

A varredura espacial utilizou o modelo probabilístico de Poisson retrospectivo no software SaTScan™ (versão 10.x), integrado ao ambiente R. Os parâmetros utilizados estão disponíveis nos arquivos `model.prm` na pasta `1 - ESPACIAL/` de cada categoria.

Configuração principal:
- Janela espacial máxima: **10% da população sob vigilância**
- Janela temporal: **50% do período**
- Simulações Monte Carlo: **999** (p < 0,05)

---

## Análise de tendências temporais

A tendência do IPA foi estimada por **regressão de Prais-Winsten** com correção AR(1), verificada pelo teste de Durbin-Watson. A projeção determinística para 2025–2030 foi ancorada no valor ajustado de 2024 e assume continuidade das condições observadas no período histórico.

---

## Fonte dos dados

- **Casos de malária:** SIVEP-Malária (Sistema de Informação de Vigilância Epidemiológica da Malária), obtidos via Lei de Acesso à Informação (Lei nº 12.527/2011) — Protocolo nº 25072025779202510
- **Denominadores populacionais:** DATASUS — Projeções populacionais por município, sexo e idade (Edição 2024)
- **Calibração por cor/raça:** Censos Demográficos 2010 e 2022 (IBGE/SIDRA) — modelo de calibração bifásica descrito em [referência da nota metodológica — no prelo]
- **Calibração por escolaridade:** Censo Demográfico 2000 como linha de base (IBGE/SIDRA)
- **Malha municipal:** IBGE 2020, via pacote `geobr` (R)

---

## Citação

Se utilizar estes dados ou código, por favor cite:

```
Pereira POB et al. Malária na Amazônia Ocidental: Dinâmica Espaço-Temporal
e Desigualdades (2012–2024). Revista de Saúde Pública, 2026. [no prelo]
```

DOI do repositório: [inserir após geração no Zenodo]

---

## Licença

Este repositório está licenciado sob a **MIT License** — veja o arquivo [LICENSE](LICENSE) para detalhes.

---

## Aspectos éticos

O estudo utilizou dados secundários de domínio público, anonimizados, dispensando apreciação pelo Sistema CEP/CONEP nos termos do Art. 1º, parágrafo único, da Resolução CNS nº 510/2016.

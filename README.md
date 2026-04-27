# 🌍 Desafio 02 — Pipeline de Variáveis Ambientais para SDM

## 🎯 Objetivo

Construir um mini-pipeline capaz de:

- Captar dados ambientais/satelitais  
- Processar e padronizar rasters  
- Gerar variáveis ambientais prontas para modelagem SDM  

Baseado no arquivo de ocorrências:
- ocorrencias_canola_sdm_desafio.csv
  
---

## 📂 Dados de Entrada

Arquivo contendo:

- `decimalLatitude` — latitude do ponto  
- `decimalLongitude` — longitude do ponto  
- `species` — espécie/cultura analisada  
- `sp` — variável resposta (1 = presença, 0 = pseudo-ausência)  
- `label` — descrição do tipo de registro  

---

## 📍 Área de Estudo

Sugestão:

- Norte: -20  
- Oeste: -58  
- Sul: -35  
- Leste: -43  

Argumento:

```bash
--area="-20,-58,-35,-43"
```

## 📅 Período
- 2025-04-01 até 2025-09-30

🌿 Variáveis Geradas
✔ Mínimo esperado
- ndvi_media_abr_ago
-ndvi_min_abr_ago
- t2m_media_abr_ago
- precipitacao_acumulada_abr_ago
- dias_geada_abr_ago
➕ Extras (opcional)
- evapotranspiração
- altitude
- uso do solo
- dias de calor

## 🛰️ Fontes de Dados

Exemplos de fontes possíveis:

- Sentinel-2 / Landsat → NDVI
- ERA5-Land → temperatura, precipitação, evapotranspiração
- SRTM / Copernicus DEM → altitude
- MapBiomas / ESA WorldCover → uso do solo

⚙️ Requisitos Técnicos

O pipeline deve demonstrar domínio sobre:

Recorte espacial
- Sistema de coordenadas (CRS)
- Resolução espacial e temporal
- Tratamento de valores NoData
- Reamostragem (resample)
- Alinhamento entre rasters
- Diferença entre dados contínuos e categóricos
📌 Observação importante
- Variáveis contínuas (NDVI, temperatura, precipitação):
-- Média, soma, interpolação (ex: bilinear)
- Variáveis categóricas (uso do solo):
-- Moda ou nearest neighbor
❌ Nunca usar interpolação contínua

🔄 Fluxo do Pipeline
1. Download dos dados
2. Recorte espacial
3. Processamento
4. Agregação temporal
5. Padronização (CRS, resolução, extensão)
6. Exportação final

## 📁 Estrutura do Projeto

project/

├── README.md

├── requirements.txt ou environment.yml

├── config.yaml

├── data/

│ ├── raw/

│ ├── interim/

│ └── processed/

├── scripts/

│ ├── 01\_download\_data.py

│ ├── 02\_process\_data.py

│ ├── 03\_generate\_predictors.py

│ └── 04\_validate\_outputs.py

├── outputs/

│ ├── maps/

│ ├── rasters/

│ └── metadata.csv

└── run\_pipeline.py

##▶️ Execução

Exemplo de execução:
python run_pipeline.py \
  --occurrences ocorrencias_canola_sdm_desafio.csv \
  --start-date 2025-04-01 \
  --end-date 2025-09-30 \
  --area "-20,-58,-35,-43" \
  --output outputs/rasters

<img width="782" height="285" alt="image" src="https://github.com/user-attachments/assets/c998dd96-b7e9-427f-a8f8-a612b48b5454" />

🧪 Validação
- Visualização no QGIS ou equivalente
- Conferência de alinhamento espacial
- Verificação de CRS
- Checagem de valores NoData

📄 Entregáveis

Ao final, devem ser entregues:

- Código reprodutível
- README
- Arquivos raster (GeoTIFF ou NetCDF)
- Tabela de metadados
- Prints ou mapas (validação)
- Relatório técnico (3–6 páginas)

📈 Critérios de Avaliação
- Processamento geoespacial
- Qualidade dos dados
- Organização do código
- Reprodutibilidade
- Clareza do relatório

🧠 O que será avaliado
- Escolha das fontes de dados
- Correta padronização dos rasters
- Tratamento de NoData
- Alinhamento espacial
- Diferença entre dados contínuos e categóricos
- Validação visual
- Clareza na explicação técnica

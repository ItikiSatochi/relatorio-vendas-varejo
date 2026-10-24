# Relatório e Painel de Vendas no Varejo

Análise analítica e preventiva de 24 meses de vendas no varejo, de jan/2024 a dez/2025. A base tem 89.904 pedidos, e o projeto vai do arquivo bruto até alertas acionáveis.

O projeto publica duas páginas estáticas:

| Página | Caminho | Para que serve |
| --- | --- | --- |
| **Relatório executivo** | `/` | Leitura linear: sumário, qualidade dos dados, desempenho, mix, riscos, previsão e plano de 90 dias. |
| **Painel dinâmico** | `/painel/` | Exploração com 5 filtros (ano, região, categoria, canal e segmento) e 3 abas: visão executiva, riscos e alertas, qualidade dos dados. |

## Principais resultados

- **Receita líquida:** Rs 804,1 mi em 24 meses, com margem líquida de 22,3%. Em 2025 foi Rs 401,1 mi, 0,5% abaixo de 2024.
- **Fim de ano:** o 4º trimestre de 2025 caiu 3,5% (novembro −4,4%, dezembro −6,6%), no trimestre mais forte do ano.
- **Perdas:** 9,2% dos pedidos viram cancelamento, devolução ou estorno, somando Rs 80,0 mi brutos.
- **Desconto:** a margem cai de 27,2% (desconto de 0 a 5%) para 14,8% (desconto de 30 a 60%).
- **Nota do cliente:** pedidos com nota 1 ou 2 viram devolução em 55% dos casos.
- **Concentração:** Punjab responde por 51% da receita (HHI 3.508).
- **Riscos:** o projeto mapeia 11 riscos, cada um com um gatilho mensurável e uma ação preventiva.

## Como foi construído

1. **Diagnóstico de qualidade:** perfil das 23 colunas em Python (pandas).
2. **ETL auditável:** 29 regras registradas; 99,9% da base preservada (80 linhas removidas) e 40,8 mil grafias padronizadas. O valor da venda foi a fonte de verdade para reconciliar preço e quantidade, com erro mediano de Rs 0,17.
3. **Modelagem:** Power Query M em 3 camadas e 37 medidas DAX, validadas contra os números do Python.
4. **Análise preventiva:**
   - controle estatístico (média ± 2σ);
   - índice sazonal, HHI e Pareto;
   - previsão por tendência linear × sazonalidade, com intervalo de 95%.
5. **Publicação:** este repositório. O conteúdo é HTML, CSS, SVG e D3, sem framework e sem build.

## Estrutura

```
.
├── index.html            # Relatório executivo (página única)
├── painel/
│   ├── index.html        # Painel dinâmico
│   ├── d3.min.js         # D3 v7.9.0 (licença ISC), servido localmente
│   └── data/             # Agregações pré-calculadas em CSV, sem dados pessoais
│       ├── kpi_slices.csv       # KPIs por combinação de filtros
│       ├── monthly_slices.csv   # Série mensal por combinação de filtros
│       ├── product_slices.csv   # Produtos por combinação de filtros
│       ├── forecast.csv         # Realizado, tendência, previsão e limites
│       ├── alerts.csv           # Registro de riscos, gatilhos e ações
│       ├── quality.csv          # Auditoria das regras de ETL
│       └── ...                  # Sazonalidade, desconto, nota e clientes
├── vercel.json           # Configuração de site estático
└── README.md
```

## Como rodar localmente

O painel carrega os CSVs com `fetch`, por isso precisa de um servidor local. Abrir o arquivo direto no navegador não funciona.

```bash
python3 -m http.server 8000
# relatório: http://localhost:8000
# painel:    http://localhost:8000/painel/
```

Os filtros ficam na URL. Por exemplo, `/painel/?year=2024&region=Punjab#riscos` abre já filtrado.

## Deploy

O projeto é importado na Vercel com framework "Other", sem comando de build e com a raiz como diretório de saída. Cada push na `main` publica uma nova versão.

## Privacidade

O repositório contém apenas agregações. Não há nomes, identificadores de cliente nem a base linha a linha. No relatório, o botão **Ocultar valores** borra os valores absolutos para apresentações.

## Ecossistema

Google Sheets (captura) → n8n (verificação dos gatilhos e disparo de alertas) → Power BI (análise executiva). Este site serve de vitrine pública do projeto.

## Autor

**Diego Satochi**: Advanced Data Analytics, automação e IA aplicada a negócios.

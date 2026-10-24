# Relatório de Vendas no Varejo

Análise analítica e preventiva de 24 meses de vendas (jan/2024 a dez/2025, 89.904 pedidos), publicada como site estático.

## Conteúdo

- Sumário executivo e KPIs de 2024 contra 2025
- Qualidade dos dados (29 regras de ETL auditáveis)
- Desempenho mensal, mix de categorias e concentração
- Faixa de controle estatístico (média ± 2σ) e 11 riscos com gatilho de alerta
- Previsão do 1º trimestre de 2026 e plano de ação de 90 dias

A página tem tema claro e escuro e um botão "Ocultar valores" que borra os valores absolutos em rúpias.

## Como rodar

É um único `index.html` sem build. Para ver localmente, abra o arquivo no navegador.

## Deploy

O projeto é importado na Vercel sem framework, sem comando de build e com o diretório de saída na raiz. Cada push na `main` publica uma nova versão em produção.

## Autor

Diego Satochi · Advanced Data Analytics, automação e IA aplicada a negócios.

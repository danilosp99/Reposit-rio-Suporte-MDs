# SKILLS.md — Skills e Padrões de Código

## Leitura de Bases S3
- Sempre verificar schema antes de agregações
- Usar inferSchema=False em PySpark quando possível
- Documentar colunas-chave utilizadas

## Métricas de Crédito
- **FPD15:** % contratos com atraso ≥ 15 dias nos primeiros 30 dias de vida
- **FPD30:** % contratos com atraso ≥ 30 dias nos primeiros 60 dias de vida
- **Over:** carteira em atraso sobre carteira ativa
- **Safra:** conjunto de contratos originados em determinado período

## Padrão de Visualização
- Paleta: seguir padrão Creditas (verde, cinza, vermelho para alertas)
- Sempre incluir anotações de volume nas barras
- Exportar em Excel para apresentações executivas

## Convenções de Nomenclatura
- Arquivos de análise: `YYYYMMDD_descricao_analise.ipynb`
- Bases processadas: `base_<produto>_<safra>_<versao>.parquet`
- Outputs: `output_<iniciativa>_<data>.xlsx`

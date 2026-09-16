# 🗂️ TASK — Orquestrador de Projetos · Risco de Crédito

> **Como usar:** Cole este arquivo na raiz do seu workspace e abra uma nova sessão no Claude Code.  
> O Claude irá executar as etapas abaixo em sequência, pausando para confirmar cada fase.

---

## ⚙️ INSTRUÇÕES PARA O CLAUDE CODE

Você é um orquestrador de projetos especializado em **Risco de Crédito, Políticas de Crédito e Analytics**.  
Ao receber este arquivo, execute as etapas na ordem abaixo. Não pule etapas. Confirme cada uma antes de avançar.

---

## ETAPA 1 — Estrutura do Projeto

### 1.1 · Localizar a pasta de trabalho

1. Execute `pwd` para identificar o diretório atual.
2. Liste os arquivos com `ls -la` para confirmar o contexto.
3. Se o diretório não parecer correto (ex: raiz do sistema, pasta genérica), pergunte ao usuário:
   > "Não consegui identificar a pasta do projeto. Qual é o caminho completo onde devemos criar a estrutura?"
4. Confirme com o usuário antes de criar qualquer coisa:
   > "Vou criar a estrutura na pasta: `<caminho>`. Pode confirmar?"

### 1.2 · Criar estrutura de pastas

Após confirmação, crie a seguinte estrutura dentro da pasta do projeto:

```
<pasta_projeto>/
├── .claude/
│   └── settings.json        ← autorizações base (sem prompts de permissão)
├── 1 - Documentações/
│   └── arquivos_claude/
│       ├── CLAUDE.md
│       ├── MEMORY.md
│       ├── AGENTS.md
│       ├── SKILLS.md
│       └── TASK.md          ← cópia deste arquivo
├── 2 - Bases/
└── 3 - Analytics/
```

**Conteúdo do `.claude/settings.json`:**
```json
{
  "permissions": {
    "allow": [
      "Write",
      "Edit",
      "Bash(New-Item *)",
      "Bash(Remove-Item *)",
      "Bash(Copy-Item *)",
      "Bash(C:\\ProgramData\\anaconda3\\python.exe *)"
    ]
  }
}
```

**Conteúdo inicial dos arquivos em `arquivos_claude/`:**

#### `CLAUDE.md`
```markdown
# CLAUDE.md — Contexto da Sessão

## Papel
Você é um especialista em Risco de Crédito, Políticas de Crédito, Pricing e Analytics.
Seu foco é apoiar análises, modelagem e documentação de iniciativas da área de crédito.

## Contexto Técnico
- Ambiente: Jupyter / VSCode + Python
- Stack: pandas, PySpark, boto3, SQLAlchemy, seaborn, plotly, openpyxl
- Dados: S3 data lake, Redshift Serverless
- Domínios: FPD, Over, Inadimplência, TopUp, BHV, Auto Equity, MDM

## Regras da Sessão
- Sempre use blocos de código completos e prontos para rodar
- Inclua logging detalhado (print statements) em cada etapa
- Outputs devem ser compatíveis com Excel quando solicitado
- Siga as convenções de nomenclatura já existentes no projeto
- Consulte MEMORY.md antes de responder sobre decisões passadas
- Registre decisões importantes em MEMORY.md
```

#### `MEMORY.md`
```markdown
# MEMORY.md — Registro de Decisões

> Atualize este arquivo ao longo do projeto com decisões, descobertas e contexto relevante.

## Decisões Técnicas
<!-- Ex: "Optamos por usar FPD15 como métrica principal pois o FPD30 ainda não matura no período" -->

## Anomalias Encontradas
<!-- Ex: "Safra Mai/24 apresentou spike de FPD fora do padrão — investigar outlier" -->

## Próximos Passos
<!-- Lista viva de pendências -->

## Histórico de Alterações
| Data | Decisão | Por quê |
|------|---------|---------|
|      |         |         |
```

#### `AGENTS.md`
```markdown
# AGENTS.md — Agentes e Responsabilidades

## Agentes desta Sessão

### 🔍 Analista de Dados
**Responsabilidade:** Exploração, limpeza e agregação de bases  
**Aciona quando:** Precisar ler CSV/Parquet do S3, fazer EDA, gerar distribuições

### 📊 Analista de Política
**Responsabilidade:** Definição de regras, cortes, segmentações  
**Aciona quando:** Precisar avaliar impacto de política, testar hipóteses de corte

### 📈 Analista de Performance
**Responsabilidade:** Monitoramento pós-implantação, FPD, Over, curvas de maturação  
**Aciona quando:** Precisar de análise D+30, D+60, D+90, Shift-Share, bridge

### 📝 Documentador
**Responsabilidade:** Atualizar MEMORY.md, gerar ata final, registrar decisões  
**Aciona quando:** Ao final de cada etapa ou quando uma decisão importante for tomada
```

#### `SKILLS.md`
```markdown
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
```

### 1.3 · Confirmação da Etapa 1

Após criar todos os arquivos, responda exatamente:

```
✅ Etapa 1️⃣ Concluída — Estrutura do Projeto criada em: <caminho_completo>

📁 Criado:
   .claude/
      └── settings.json
   1 - Documentações/arquivos_claude/
      ├── CLAUDE.md
      ├── MEMORY.md
      ├── AGENTS.md
      ├── SKILLS.md
      └── TASK.md
   2 - Bases/
   3 - Analytics/

Pronto para a Etapa 2️⃣ — vou coletar as informações do projeto.
```

---

## ETAPA 2 — Briefing da Iniciativa

Colete as informações abaixo **uma a uma**, em sequência. Não apresente todas as perguntas de uma vez.

### 2.1 · Coleta de dados

Pergunte em sequência:

```
1. 📌 Nome da Iniciativa:
2. 📝 Descrição resumida (o que é, por que estamos fazendo):
3. 🏷️ Tipo de Iniciativa:
      [1] Política de Crédito
      [2] Manutenção / Ajuste
      [3] Troca / Atualização de Modelo
      [4] Campanha / Pricing
      [5] Acompanhamentos
4. 📅 Data de Início (DD/MM/AAAA):
5. 🏁 Data Prevista de Conclusão (DD/MM/AAAA):
6. 👤 Relator — quem pediu a demanda?
7. 🛠️ Responsável — quem irá executar?
8. 🎯 KPI esperado (ex: FPD15 ≤ 4,5% | Aprovação +8pp | Over estável):
9. 🔗 Contexto adicional / Hipótese principal (opcional — pode pular):
10. 📋 Etapas planejadas para execução (ex: 1. Análise exploratória | 2. Correção de filtros | 3. Validação):
```

### 2.2 · Confirmação do Briefing

Após coletar tudo, exiba um resumo formatado:

```
📋 BRIEFING DA INICIATIVA
─────────────────────────────────────────────
  Nome:         <valor>
  Tipo:         <valor>
  Descrição:    <valor>
  Início:       <valor>
  Conclusão:    <valor>
  Relator:      <valor>
  Responsável:  <valor>
  KPI Esperado: <valor>
  Hipótese:     <valor>
  Etapas:       <lista de etapas planejadas>
─────────────────────────────────────────────
Confirmar e avançar? (s/n)
```

### 2.3 · Criar ATA.html com o briefing

Após confirmação, crie o arquivo `1 - Documentações/ATA.html` com o template abaixo.

**Regras de geração:**
- A tabela de progresso contém **exatamente as etapas definidas pelo usuário no briefing** (pergunta 10) — sem etapas fixas ou padrão
- O total da barra = número de etapas do briefing
- Status inicial de todas as etapas: `⬜ Pendente`
- Barra de progresso começa em 0%
- Substitua todos os `<placeholders>` pelos valores coletados no briefing

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>ATA — <NOME DA INICIATIVA></title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: 'Segoe UI', system-ui, sans-serif; background: #f4f5f7; color: #1a1a2e; padding: 32px 16px; }
    .card { background: #fff; border-radius: 12px; box-shadow: 0 2px 12px rgba(0,0,0,.08); padding: 32px; max-width: 900px; margin: 0 auto 24px; }
    .header { border-bottom: 2px solid #f0f0f0; padding-bottom: 24px; margin-bottom: 24px; }
    .header h1 { font-size: 1.5rem; font-weight: 700; color: #1a1a2e; margin-bottom: 12px; }
    .meta-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 12px; font-size: .875rem; }
    .meta-item { display: flex; flex-direction: column; gap: 2px; }
    .meta-label { font-weight: 600; color: #6b7280; text-transform: uppercase; font-size: .7rem; letter-spacing: .05em; }
    .meta-value { color: #1a1a2e; }
    .badge { display: inline-flex; align-items: center; gap: 6px; padding: 4px 12px; border-radius: 999px; font-size: .8rem; font-weight: 600; }
    .badge-green  { background: #d1fae5; color: #065f46; }
    .badge-yellow { background: #fef9c3; color: #854d0e; }
    .badge-red    { background: #fee2e2; color: #991b1b; }
    h2 { font-size: 1rem; font-weight: 700; color: #374151; margin-bottom: 14px; }
    .progress-bar-bg { background: #e5e7eb; border-radius: 999px; height: 14px; overflow: hidden; }
    .progress-bar-fill { height: 100%; border-radius: 999px; background: linear-gradient(90deg, #10b981, #059669); }
    .progress-label { font-size: .85rem; color: #6b7280; margin-top: 6px; }
    table { width: 100%; border-collapse: collapse; font-size: .875rem; }
    th { background: #f9fafb; text-align: left; padding: 10px 12px; font-size: .75rem; font-weight: 600; color: #6b7280; text-transform: uppercase; letter-spacing: .05em; border-bottom: 1px solid #e5e7eb; }
    td { padding: 10px 12px; border-bottom: 1px solid #f3f4f6; vertical-align: top; }
    tr:last-child td { border-bottom: none; }
    tr:hover td { background: #fafafa; }
    .status-done    { color: #059669; font-weight: 600; }
    .status-pending { color: #9ca3af; }
    .status-progress{ color: #d97706; font-weight: 600; }
    .status-blocked { color: #dc2626; font-weight: 600; }
    .step-num { font-weight: 700; color: #6b7280; }
    .empty-note { color: #9ca3af; font-style: italic; font-size: .875rem; }
    footer { text-align: center; font-size: .75rem; color: #9ca3af; margin-top: 8px; }
  </style>
</head>
<body>

<div class="card">
  <div class="header">
    <h1><NOME DA INICIATIVA></h1>
    <div class="meta-grid">
      <div class="meta-item">
        <span class="meta-label">Status</span>
        <span><span class="badge badge-yellow">🟡 Em andamento</span></span>
      </div>
      <div class="meta-item"><span class="meta-label">Tipo</span><span class="meta-value"><TIPO></span></div>
      <div class="meta-item"><span class="meta-label">Relator</span><span class="meta-value"><RELATOR></span></div>
      <div class="meta-item"><span class="meta-label">Responsável</span><span class="meta-value"><RESPONSÁVEL></span></div>
      <div class="meta-item"><span class="meta-label">Início</span><span class="meta-value"><DATA_INICIO></span></div>
      <div class="meta-item"><span class="meta-label">Prazo</span><span class="meta-value"><DATA_FIM></span></div>
    </div>
  </div>
  <div style="margin-bottom:20px;">
    <h2>Objetivo</h2>
    <p style="font-size:.9rem;color:#374151;line-height:1.6;"><DESCRIÇÃO></p>
  </div>
  <div>
    <h2>KPI Esperado</h2>
    <p style="font-size:.9rem;color:#374151;"><KPI></p>
  </div>
</div>

<div class="card">
  <h2>Progresso das Etapas</h2>
  <div style="margin-bottom:16px;">
    <div class="progress-bar-bg">
      <div class="progress-bar-fill" style="width: 0%;"></div>
    </div>
    <div class="progress-label">0% concluído — 0 de <TOTAL_ETAPAS> etapas</div>
  </div>
  <table>
    <thead>
      <tr><th>#</th><th>Etapa</th><th>Status</th><th>Data</th><th>Observação</th></tr>
    </thead>
    <tbody>
      <!-- Gerar uma <tr> por etapa do briefing -->
      <tr>
        <td class="step-num">1</td>
        <td><ETAPA_1></td>
        <td class="status-pending">⬜ Pendente</td>
        <td></td><td></td>
      </tr>
      <!-- repetir para cada etapa -->
    </tbody>
  </table>
</div>

<div class="card">
  <h2>Discovery — O que foi feito nesta sessão</h2>
  <div style="display:flex;flex-direction:column;gap:16px;margin-top:4px;">
    <!-- Gerar um bloco por etapa concluída, preenchendo conforme o projeto avança -->
    <!-- Exemplo de bloco: -->
    <!--
    <div style="border-left:3px solid #10b981;padding:10px 16px;background:#f0fdf4;border-radius:0 8px 8px 0;">
      <p style="font-size:.8rem;font-weight:700;color:#059669;text-transform:uppercase;letter-spacing:.05em;margin-bottom:4px;">Etapa N · <NOME_DA_ETAPA></p>
      <ul style="font-size:.875rem;color:#374151;line-height:1.7;padding-left:18px;">
        <li>O que foi feito, descoberto ou decidido</li>
      </ul>
    </div>
    -->
    <p class="empty-note">Nenhuma atividade registrada ainda.</p>
  </div>
</div>

<div class="card">
  <h2>Texto Resumido para Trello</h2>
  <!-- Cole este texto na descrição do card do Trello ao concluir o projeto -->
  <div style="background:#f9fafb;border:1px solid #e5e7eb;border-radius:8px;padding:16px;font-size:.875rem;color:#374151;line-height:1.7;white-space:pre-wrap;font-family:monospace;">**<NOME DA INICIATIVA>**
Solicitante: <RELATOR> | Responsável: <RESPONSÁVEL> | Data: <DATA_INICIO>

**Objetivo**
<DESCRIÇÃO RESUMIDA EM 2-3 LINHAS>

**O que foi feito**
<- Bullet por etapa concluída com resultado principal>

**Status:** <🟡 Em andamento | ✅ Concluído> (<N>/<TOTAL_ETAPAS> etapas)</div>
</div>

<div class="card">
  <h2>Registro de Decisões</h2>
  <p class="empty-note">Nenhuma decisão registrada.</p>
</div>

<div class="card">
  <h2>Resultado Real</h2>
  <p class="empty-note">Preencher após implantação e monitoramento.</p>
</div>

<footer>
  Documento gerado automaticamente pelo orquestrador TASK.md · Última atualização: <DATA_GERACAO>
</footer>

</body>
</html>
```

**Ao atualizar etapas (`/etapa`) ou decisões (`/decisao`):** edite diretamente o arquivo `ATA.html` —
- Troque a classe CSS da célula de status (`status-pending` → `status-done` / `status-progress` / `status-blocked`)
- Preencha o texto de status, data e observação na `<td>` correspondente
- Recalcule `width` da `.progress-bar-fill` e o texto da `.progress-label`
- Para status `🟢 Concluído`: troque a classe do badge para `badge-green`

### 2.4 · Confirmação da Etapa 2

Após criar o ATA.html, responda:

```
✅ Etapa 2️⃣ Concluída — Briefing registrado

📄 ATA.html criada em: 1 - Documentações/ATA.html

Seu projeto está configurado. Aqui estão os próximos comandos disponíveis:

  📌 /etapa <número> <status>  → Marcar etapa como concluída
                                  Ex: /etapa 1 ok
                                  Ex: /etapa 3 bloqueado "aguardando dados"

  📊 /progresso                → Ver status atual de todas as etapas

  📝 /decisao "<texto>"        → Registrar uma decisão no ATA.html

  📈 /resultado "<kpi_real>"   → Registrar resultado pós-implantação

  📋 /ata                      → Gerar resumo executivo da ata atual

  🔄 /atualizar                → Re-ler ATA.html e exibir status completo
```

---

## ETAPA 3 — Gestão de Progresso (Comandos Ativos)

Durante a execução do projeto, responda aos comandos abaixo sempre que o usuário os invocar.

### `/etapa <n> <status> ["observação"]`

Atualize a linha correspondente na tabela de progresso do ATA.md:

- `ok` → `✅ Concluída` + data de hoje
- `em_andamento` → `🔄 Em andamento` + data de hoje
- `bloqueado` → `🔴 Bloqueado` + observação
- `na` → `➖ N/A`

Recalcule o progresso e atualize a barra com base no total de etapas do briefing (não use 15 fixo):

```
Progresso: ████████░░ 53% (4/7 etapas)
```

- Total de etapas = número de etapas que o usuário definiu no briefing
- Percentual = (concluídas / total) × 100, arredondado
- Barra de 10 blocos: cada `█` = 10%. Use `░` para pendentes.
- Etapas com status `➖ N/A` não contam no denominador.

---

### `/progresso`

Exiba a tabela completa do ATA.md com o status atual de cada etapa e a barra de progresso.

---

### `/decisao "<texto>"`

Adicione uma linha na tabela "Registro de Decisões" do ATA.md com a data de hoje e o responsável da sessão.

---

### `/resultado "<kpi_realizado>"`

Preencha a seção "Resultado Real" do ATA.md e calcule a diferença vs KPI esperado.

---

### `/ata`

Gere um resumo executivo em formato limpo para ser colado em Slack ou e-mail:

```
📋 ATA · <NOME DA INICIATIVA>
Data: <hoje> | Responsável: <responsável>

OBJETIVO
<descrição em 1-2 linhas>

PROGRESSO
<barra> <pct>% — <n> de <total do briefing> etapas concluídas
Última etapa: <etapa mais recente concluída>

PRÓXIMOS PASSOS
• <próxima etapa pendente>
• <próxima etapa pendente>

KPI ESPERADO → <kpi>
KPI REALIZADO → <resultado ou "em monitoramento">
```

---

## REFERÊNCIA RÁPIDA — Etapas do Projeto

As etapas de referência são as definidas pelo usuário no briefing (pergunta 10).
Não use uma lista fixa — leia as etapas diretamente da seção "Etapas Planejadas" do ATA.md do projeto atual.

---

*TASK.md v1.1 · Risco de Crédito · Creditas*

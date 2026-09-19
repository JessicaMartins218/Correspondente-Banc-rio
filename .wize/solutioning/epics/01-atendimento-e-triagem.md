---
epic_id: 01-atendimento-e-triagem
status: ready
owner: Maria Hill + Tony Stark
linked_prd: E01
priority: 1
---

# Epic 01: Atendimento Receptivo, Prospecção Ativa (Outbound) e Triagem com Consentimento LGPD

## Outcome
O cliente ou contato prospectado interage no WhatsApp da JM Consultoria com acolhimento humanizado e segurança jurídica, fornece consentimento LGPD auditável, valida seu CPF e define o produto de crédito desejado (FGTS, Consignado CLT ou INSS), com canal de transbordo imediato para operadores humanos.

## Stories
- **E01-S01:** Recepção do Webhook do WhatsApp e Mensagem de Boas-Vindas com Consentimento LGPD (AC-01-1, AC-01-2)
- **E01-S02:** Validação Algorítmica de CPF e Triagem de Produto de Crédito (AC-01-3)
- **E01-S03:** Motor de Disparo Ativo de Base de Contatos com Fila e Cadência Anti-Banimento (AC-01-4)
- **E01-S04:** Mecanismo de Transbordo Humano e Pausa de Automação para Operadores (AC-01-5)

## Dependencies
- Instância ativa de gateway do WhatsApp (Evolution API / Cloud API) conectada ao número da JM Consultoria.
- Banco de dados de sessões conversacionais e tabela de logs de consentimento LGPD.

## Success
Taxa de consentimento LGPD ≥ 85%; tempo de resposta inicial do bot p95 ≤ 1,5s; zero banimentos em disparos ativos para bases de leads.

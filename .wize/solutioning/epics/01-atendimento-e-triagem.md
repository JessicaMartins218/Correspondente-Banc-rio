---
epic_id: 01-atendimento-e-triagem
status: ready
owner: Tony Stark + Maria Hill
linked_prd: E01
trigger_map_row: 1
priority: 1
---

# Epic 01: Atendimento Inicial, Consentimento LGPD e Triagem

## Outcome
O cliente entra em contato pelo WhatsApp, recebe resposta imediata com acolhimento da JM Consultoria, fornece consentimento formal conforme a LGPD e realiza a validação de CPF e triagem do perfil de crédito em menos de 2 minutos.

## Stories
- **E01-S01:** Recepção do Webhook do WhatsApp e Mensagem de Boas-Vindas com Consentimento LGPD (AC-01-1, AC-01-2)
- **E01-S02:** Validação Algorítmica de CPF e Consulta Preliminar de Elegibilidade de Margem (AC-01-3, AC-01-4)
- **E01-S03:** Mecanismo de Transbordo Humano e Pausa de Automação para Operadores (AC-01-5)

## Dependencies
- Configuração do WhatsApp Cloud API (número verificado, webhooks ativos e tokens da Meta).
- Banco de dados de sessões conversacionais e tabela de logs de consentimento LGPD.

## Success
Taxa de consentimento LGPD ≥ 85% dos usuários que iniciam contato; tempo de resposta do bot p95 ≤ 1.5s; acionamento suave de transbordo quando solicitado.

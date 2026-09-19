---
epic_id: 03-coleta-e-digitacao-bancaria
status: ready
owner: Maria Hill + Tony Stark
linked_prd: E03
priority: 3
---

# Epic 03: Coleta Cadastral e Digitação Automatizada da Proposta no Portal do Banco

## Outcome
O cliente fornece dados cadastrais complementares no WhatsApp, com validação obrigatória de conta bancária de mesma titularidade (bloqueio de contas de terceiros conforme BACEN), e o robô preenche e submete a proposta de forma 100% autônoma no portal web do banco parceiro via RPA.

## Stories
- **E03-S01:** Coleta Conversacional de Dados Pessoais e Validação de Conta Bancária de Mesma Titularidade (AC-03-1, AC-03-2)
- **E03-S02:** Digitação Automatizada da Proposta no Portal Web do Banco via RPA (AC-03-3, AC-03-5)
- **E03-S03:** Tratamento de Pendências de Digitação e Mensagens de Erro Amigáveis (AC-03-4)

## Dependencies
- Epic 02 concluído (proposta selecionada pelo cliente e sessão autenticada no banco).
- Motor de validação de agência, conta e chave PIX com verificação de CPF.

## Success
100% dos contratos digitados sem erro de digitação de campos; bloqueio de 100% das tentativas de pagamento em contas de terceiros; tempo de preenchimento e submissão no portal do banco ≤ 45 segundos.

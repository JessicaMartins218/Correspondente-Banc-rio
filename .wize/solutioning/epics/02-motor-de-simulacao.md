---
epic_id: 02-motor-de-simulacao
status: ready
owner: Tony Stark + Maria Hill
linked_prd: E02
trigger_map_row: 2
priority: 2
---

# Epic 02: Motor de Simulação Multibancos e Apresentação de Propostas

## Outcome
O cliente escolhe o produto de crédito desejado (INSS, FGTS, etc.) e recebe instantaneamente uma lista clara, transparente e comparativa das melhores propostas dos bancos parceiros, podendo ajustar parcelas e prazos ou selecionar a proposta ideal no chat.

## Stories
- **E02-S01:** Integração com APIs de Simulação dos Bancos e Cálculo de CET e Parcelas (AC-02-1)
- **E02-S02:** Formatação Visual e Comparativo Interativo de Propostas no WhatsApp (AC-02-2)
- **E02-S03:** Customização de Prazos/Valores e Reserva de Tabela com Congelamento de Proposta (AC-02-3, AC-02-4)

## Dependencies
- Epic 01 concluído (sessão ativa e CPF triado).
- Credenciais e rotas de integração das APIs/tabelas de promotoras e bancos conveniados.

## Success
Simulação completa retornada em tempo real (tempo de resposta agregado ≤ 3s); taxa de abandono na tela de propostas ≤ 15%.

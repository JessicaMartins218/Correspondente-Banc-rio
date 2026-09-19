---
epic_id: 05-acompanhamento-e-liquidacao
status: ready
owner: Tony Stark + Maria Hill
linked_prd: E05
trigger_map_row: 5
priority: 5
---

# Epic 05: Averbação, Desembolso Financeiro e Notificação em Tempo Real

## Outcome
A proposta assinada é transmitida para a esteira bancária e averbada junto ao órgão responsável (Dataprev/INSS/Caixa). Assim que o pagamento (PIX/TED) é efetuado, o cliente recebe notificação comemorativa imediata no WhatsApp com o comprovante de pagamento e cópia da CCB, encerrando a jornada com pesquisa de satisfação.

## Stories
- **E05-S01:** Transmissão da Proposta para a Esteira Bancária e Notificação de Averbação em Andamento (AC-05-1)
- **E05-S02:** Tratamento de Recusa/Pendência de Averbação com Alerta ao Operador e ao Cliente (AC-05-2)
- **E05-S03:** Webhook de Confirmação de Liquidação Financeira e Emissão de Comprovante (AC-05-3, AC-05-4)
- **E05-S04:** Pesquisa de Satisfação NPS Conversacional no WhatsApp e Encerramento da Jornada (AC-05-5)

## Dependencies
- Epic 04 concluído (contrato assinado e biometria aprovada).
- Webhooks configurados para recepção de eventos de averbação e pagamento das instituições financeiras parceiras.

## Success
Tempo entre confirmação do pagamento e envio do WhatsApp com comprovante ≤ 30 segundos; índice de resposta ao NPS ≥ 40% com meta de NPS ≥ 75.

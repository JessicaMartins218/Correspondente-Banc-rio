---
epic_id: 05-acompanhamento-e-liquidacao
status: ready
owner: Maria Hill + Tony Stark
linked_prd: E05
priority: 5
---

# Epic 05: Acompanhamento de Esteira, Confirmação de Liquidação e Pós-Venda

## Outcome
O robô consulta periodicamente o status da proposta no portal do banco, avisa o cliente no WhatsApp a cada atualização (em análise, averbado e pago/PIX creditado), coleta avaliação NPS de satisfação, aciona a régua de relacionamento de pós-venda (30, 60, 90 dias) e fornece o dashboard diário de contratos pagos para a JM Consultoria acompanhar a meta de 15 contratos/dia.

## Stories
- **E05-S01:** Monitoramento Automatizado de Status da Proposta no Portal do Banco (AC-05-1)
- **E05-S02:** Notificação em Tempo Real de Averbação e Confirmação de Pagamento/PIX (AC-05-2)
- **E05-S03:** Módulo de Pós-Venda, Pesquisa NPS e Régua de Relacionamento Futuro (AC-05-3, AC-05-4)
- **E05-S04:** Dashboard Operacional e Relatório Diário de Conversão (Meta de 15 Contratos/Dia) (AC-05-5)

## Dependencies
- Epic 04 concluído (contrato formalizado pelo cliente).
- Rotina de cron/job agendada para pooling do portal do banco e consolidação de relatórios às 19h/20h.

## Success
Notificação de pagamento enviada em até 2 minutos após identificação no portal; taxa de resposta ao NPS ≥ 40%; visibilidade diária exata do atingimento da meta de 15 contratos/dia (10 FGTS/CLT e 5 INSS).

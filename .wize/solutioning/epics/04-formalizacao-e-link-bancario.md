---
epic_id: 04-formalizacao-e-link-bancario
status: ready
owner: Maria Hill + Tony Stark
linked_prd: E04
priority: 4
---

# Epic 04: Captura do Link de Formalização do Banco e Condução da Assinatura no WhatsApp

## Outcome
Assim que a proposta é digitada no portal do banco, o robô captura o link de formalização gerado pela própria instituição, envia imediatamente ao cliente no WhatsApp com orientações claras para a biometria facial e assinatura da CCB no ambiente oficial do banco, e dispara réguas de reengajamento caso a assinatura fique pendente.

## Stories
- **E04-S01:** Extração Automatizada do Link de Formalização Gerado no Portal do Banco (AC-04-1)
- **E04-S02:** Envio do Link no WhatsApp com Orientações para Biometria Facial e Assinatura de CCB (AC-04-2, AC-04-3)
- **E04-S03:** Régua de Lembretes e Reengajamento para Assinatura Pendente e Expiração de Link (AC-04-4, AC-04-5)

## Dependencies
- Epic 03 concluído (proposta digitada com sucesso e confirmada pelo portal bancário).
- Serviço de agendamento de jobs para monitoramento do prazo de 2h/24h de assinatura.

## Success
Link de formalização extraído e enviado em ≤ 5 segundos após a finalização da digitação; aumento de 20% na taxa de conversão final por meio dos lembretes automáticos de assinatura; 0 falhas no redirecionamento para o ambiente seguro do banco.

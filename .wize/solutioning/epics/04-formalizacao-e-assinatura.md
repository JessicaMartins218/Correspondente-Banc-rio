---
epic_id: 04-formalizacao-e-assinatura
status: ready
owner: Tony Stark + Maria Hill
linked_prd: E04
trigger_map_row: 4
priority: 4
---

# Epic 04: Formalização Digital, Biometria Facial e Assinatura da CCB

## Outcome
O cliente recebe via WhatsApp um link seguro de formalização digital, confere os termos e valores da Cédula de Crédito Bancário (CCB), executa a biometria facial (prova de vida com liveness) e assina o contrato eletronicamente com validade jurídica em seu smartphone.

## Stories
- **E04-S01:** Geração e Envio de Link Seguro e Efêmero de Formalização no WhatsApp (AC-04-1)
- **E04-S02:** Visualização Resumida da CCB e Termos Contratuais no Mobile Web (AC-04-2)
- **E04-S03:** Captura de Biometria Facial com Liveness e Validação de Similaridade (AC-04-3)
- **E04-S04:** Assinatura Eletrônica Juridicamente Válida com Carimbo de Tempo e Webhook de Confirmação (AC-04-4)
- **E04-S05:** Sistema de Recuperação de Propostas Pendentes e Lembretes Conversacionais (AC-04-5)

## Dependencies
- Epic 03 concluído (documentos e dados cadastrais aprovados).
- Provedor de assinatura eletrônica e biometria facial homologado (ou esteira do banco parceiro).
- Canal WhatsApp habilitado para envio de mensagens ativas e lembretes com templates aprovados.

## Success
Taxa de conclusão da formalização iniciada ≥ 80%; tempo médio de formalização mobile ≤ 3 minutos; 0 fraudes de identidade.

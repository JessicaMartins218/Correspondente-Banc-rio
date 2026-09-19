---
epic_id: 03-captura-e-validacao-documental
status: ready
owner: Tony Stark + Maria Hill
linked_prd: E03
trigger_map_row: 3
priority: 3
---

# Epic 03: Coleta, Validação Cadastral e Documentoscopia (OCR)

## Outcome
O cliente fornece os dados da conta bancária de mesma titularidade e envia as fotos do documento de identificação (RG/CNH) diretamente no WhatsApp. O sistema extrai e valida os dados com OCR e filtros antifraude em menos de 10 segundos, preparando a proposta para formalização.

## Stories
- **E03-S01:** Validação Cadastral de Dados Bancários e Bloqueio de Contas de Terceiros (AC-03-1, AC-03-2)
- **E03-S02:** Recepção de Mídia e Extração Automatizada de Dados via OCR (AC-03-3)
- **E03-S03:** Motor de Checagem de Qualidade de Imagem, Reenvio Guiado e Validação Antifraude (AC-03-4, AC-03-5)

## Dependencies
- Epic 02 concluído (`proposal_id` gerado com proposta congelada).
- Serviço de OCR e motor de validação cadastral (consulta Situação Cadastral CPF).
- Bucket seguro com criptografia em repouso (AES-256) para armazenamento efêmero de documentos.

## Success
Assertividade de extração OCR ≥ 90%; 0% de pagamentos autorizados em conta de terceiros; detecção imediata de fotos ilegíveis com retorno ao usuário em até 4 segundos.

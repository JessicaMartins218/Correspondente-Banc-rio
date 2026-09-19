---
epic_id: 02-motor-de-simulacao
status: ready
owner: Maria Hill + Tony Stark
linked_prd: E02
priority: 2
---

# Epic 02: Motor de Automação Web (RPA) para Login e Simulação nos Portais Bancários

## Outcome
O robô conecta-se de forma segura aos portais dos bancos parceiros (DSV e Prata) com as credenciais cadastradas, mantém a sessão ativa com reconexão resiliente, executa simulações precisas de crédito com base nas informações do cliente e formata uma resposta comparativa, clara e transparente no WhatsApp.

## Stories
- **E02-S01:** Cofre Seguro de Credenciais e Autenticação Automatizada (RPA) nos Portais Bancários (AC-02-1, AC-02-2)
- **E02-S02:** Motor de Simulação Headless nos Portais dos Bancos DSV e Prata (AC-02-3)
- **E02-S03:** Formatação Comparativa de Propostas no WhatsApp e Seleção de Condições pelo Cliente (AC-02-4, AC-02-5)

## Dependencies
- Epic 01 concluído (sessão ativa, consentimento LGPD e CPF validado).
- Credenciais dos portais dos bancos (DSV e Prata) salvas de forma segura no ambiente.
- Ambiente com Playwright/Puppeteer configurado para execução de navegadores headless.

## Success
Simulação extraída do portal bancário em tempo hábil (≤ 15 segundos); autenticação e reconexão automática sem quebra de sessão em 99% das tentativas; apresentação legível em smartphones com destaque de valor líquido liberado.

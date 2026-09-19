---
status: ready-for-prd
owner: Pepper Potts
created: 2026-09-19
---

# Brief — Correspondente Bancário Autônomo via WhatsApp

## Vision
Transformar a intermediação de crédito da JM Consultoria em uma operação autônoma, escalável e humanizada via WhatsApp, capaz de atender clientes receptivos e prospectar bases ativas, executar simulações multiproduto em tempo real, automatizar a digitação de propostas diretamente nos portais bancários via RPA com credenciais seguras, entregar o link oficial de formalização digital e acompanhar a jornada até o pós-venda.

## Audience
- **Primary:** Clientes tomadores de crédito (trabalhadores CLT com margem consignável ou saldo FGTS para antecipação de saque-aniversário, além de aposentados e pensionistas do INSS com interesse em margem nova, refinanciamento ou portabilidade) que buscam agilidade, taxas transparentes e contratação 100% digital sem burocracia física.
- **Secondary:** Jéssica Angie e equipe comercial da JM Consultoria (supervisão da esteira de propostas, gestão de métricas de conversão e intervenção humana em casos de exceção).
- **Stakeholders:** 
  1. **Jéssica Angie / JM Consultoria:** Maximização do volume de contratos pagos, eliminação do trabalho manual repetitivo de digitação e cumprimento das metas de escala comercial.
  2. **Instituições Financeiras Parceiras (Bancos DSV, Prata e novos conveniados):** Qualidade dos dados cadastrais, acurácia na digitação das propostas e compliance com as regras de crédito consignado.
  3. **Tomadores de Crédito:** Resposta ágil, clareza nas condições contratuais e segurança absoluta de seus dados pessoais e bancários.

## Success criteria
1. **Volume de Conversão Diária:** Atingir e sustentar a conversão mínima de 10 contratos pagos/dia para FGTS/CLT e 5 contratos pagos/dia para INSS (total de 15 contratos diários).
2. **Autonomia da Esteira:** Taxa de autoatendimento (da primeira mensagem até o envio do link de formalização gerado pelo banco) ≥ 75% nas esteiras padronizadas, sem necessidade de intervenção do consultor.
3. **Agilidade no Tempo de Resposta:** Tempo total entre a coleta dos dados básicos do cliente e a entrega do link de formalização no WhatsApp ≤ 3 minutos.
4. **Proteção do Canal de Atendimento:** Zero incidentes de bloqueio ou banimento de número no WhatsApp através de cadência controlada de mensagens e aquecimento para disparos ativos de prospecção.
5. **Conformidade e Segurança:** 100% de aderência à LGPD (dados de CPF e bancários criptografados) e proteção estrita das credenciais de acesso aos portais bancários.

## Non-goals
- **Não assumir risco de crédito próprio:** A operação atua estritamente como Correspondente no País (Corban) intermediando propostas para os bancos parceiros autorizados pelo Banco Central.
- **Não criar aplicativo móvel próprio:** A experiência do tomador é 100% concentrada no WhatsApp e na página web oficial de biometria/assinatura fornecida pelos bancos parceiros.
- **Não depender de digitação manual de dados:** O consultor humano não deve redigitar dados já fornecidos pelo cliente no WhatsApp para os bancos homologados.

## Constraints
- **Automação Web dos Portais Bancários (RPA):** Os bancos parceiros iniciais (DSV e Prata) exigem acesso por portal web com usuário e senha para simulação e digitação de propostas. A esteira precisará de um motor headless (Playwright/Puppeteer) robusto para navegação segura e extração do link de formalização.
- **Integração de Mensageria (WhatsApp):** Uso atual do WhatsApp Business requer gateway de integração (ex: Evolution API ou Z-API) para transformar o canal em um assistente programável com suporte a webhooks e mensagens interativas.
- **Prospecção Ativa (Outbound):** O futuro acionamento de bases de contatos frias exige regras estritas de cadência, rotatividade de mensagens e conformidade com as diretrizes de spam da Meta.
- **Regulatório e Compliance:** Cumprimento rigoroso das Resoluções CMN nº 3.954/2011 e 4.935/2021 do BACEN, diretrizes da Dataprev/INSS e Lei Geral de Proteção de Dados (LGPD).

## Open questions
- [ ] **(importante)** Qual gateway de mensageria para WhatsApp será conectado ao projeto nesta primeira fase (ex: Evolution API ou Z-API)? — *owner: Jéssica Angie*
- [ ] **(importante)** Criação de um usuário específico para o robô nos portais bancários (para evitar derrubar sessões simultâneas de usuários humanos)? — *owner: Jéssica Angie*
- [ ] **(nice-to-know)** Quais novos bancos serão adicionados na expansão desta semana para mapear seus portais de simulação/digitação? — *owner: Jéssica Angie*

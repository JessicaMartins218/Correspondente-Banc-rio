---
status: ready-for-validation
owner: Maria Hill
created: 2026-09-12
---

# PRD — Correspondente Bancário Inteligente via WhatsApp

## Goals
1. **Conversão de Ponta a Ponta:** Atingir taxa de conversão ≥ 25% entre a primeira mensagem recebida e o contrato pago no banco (métrica: `funnel_start_to_payout_conversion`, alvo: 25%, prazo: 90 dias após MVP).
2. **Tempo de Ciclo Operacional:** Reduzir o tempo médio de jornada do cliente (da saudação até o envio da proposta assinada para averbação) para ≤ 8 minutos no autoatendimento (métrica: `median_flow_duration`, alvo: ≤ 8 min).
3. **Automação de Atendimento:** Manter taxa de retenção resolutiva no fluxo conversacional automatizado do WhatsApp de ≥ 70%, acionando operadores humanos apenas em exceções ou pendências complexas (métrica: `bot_containment_rate`, alvo: 70%).
4. **Precisão Cadastral e Antifraude:** Manter índice de assertividade na extração documental (OCR) e validação biométrica de primeira tentativa ≥ 85% (métrica: `first_pass_approval_rate`, alvo: 85%).
5. **Transparência e Compliance:** Garantir 100% de aceite explícito dos termos de privacidade e autorização de consulta de margem/dados conforme LGPD e Resolução CMN 3.954 antes de qualquer consulta externa (métrica: `lgpd_consent_compliance`, alvo: 100%).

---

## Scope

### In scope
- **Recepção Conversacional via WhatsApp Cloud API:** Fluxo interativo humanizado com bot conversacional, menus dinâmicos e botões de resposta rápida.
- **Termo de Consentimento LGPD:** Coleta e registro auditável de aceite para tratamento de dados pessoais e consulta a birôs/margens.
- **Motor de Simulação de Propostas:** Integração com tabelas/APIs bancárias para simular prazos, valor de parcelas, taxa nominal e CET (Custo Efetivo Total) para Consignado INSS, FGTS e Crédito Pessoal.
- **Apresentação Comparativa de Propostas:** Exibição clara e comparável das melhores opções de bancos parceiros para escolha direta pelo cliente no chat.
- **Coleta e Validação Documental com OCR:** Recebimento de fotos de documento de identificação (RG/CNH) e comprovante bancário via WhatsApp, com extração automatizada de dados e validação de legibilidade.
- **Esteira de Formalização Digital:** Envio de link seguro mobile para leitura da Cédula de Crédito Bancário (CCB), biometria facial (prova de vida) e assinatura digital.
- **Acompanhamento de Status e Pagamento:** Notificação ativa por WhatsApp a cada mudança de estado da proposta (digitada, em análise, averbada, paga com envio de comprovante PIX/TED).
- **Módulo de Transbordo Humano:** Capacidade de o cliente solicitar atendimento com um consultor da JM Consultoria a qualquer momento ou transbordo automático por inconsistência de dados.

### Out of scope
- Concessão de crédito próprio / underwriting proprietário (todo o funding e crédito são originados pelos bancos parceiros conveniados).
- Aplicativo móvel para download (iOS/Android) — toda a interação ocorre no WhatsApp e webviews temporárias para biometria.
- Concessão de crédito para negativados fora das esteiras consignadas/FGTS que possuem garantia de desconto em folha ou saldo retido.
- Suporte a canais secundários de atendimento (Instagram Direct, Telegram, SMS) no primeiro release (foco 100% no canal WhatsApp).

---

## Backbone (Coarse Stories)

- **E01:** Como cliente interessado em crédito, quero iniciar uma conversa no WhatsApp e fornecer consentimento seguro, para que eu possa verificar minha elegibilidade sem burocracia.
- **E02:** Como cliente elegível, quero simular opções de empréstimo em múltiplos bancos, para que eu escolha a proposta com as melhores parcelas e menor taxa de juros.
- **E03:** Como cliente que escolheu uma proposta, quero enviar meus documentos e dados bancários pelo próprio WhatsApp, para que meus dados sejam validados rapidamente sem precisar ir a uma agência.
- **E04:** Como cliente com proposta pré-aprovada, quero assinar o contrato e realizar a biometria facial pelo celular, para que minha formalização tenha validade jurídica imediata.
- **E05:** Como cliente formalizado, quero receber atualizações em tempo real pelo WhatsApp sobre a averbação e a confirmação do pagamento, para saber exatamente quando o dinheiro caiu na minha conta.

---

## Acceptance Criteria

### E01 — Atendimento Inicial, Consentimento LGPD e Triagem

- **AC-01-1:** Dado que um novo usuário envia qualquer mensagem para o número oficial do WhatsApp, quando o sistema processa o webhook de entrada em menos de 1,5s, então responde com mensagem de boas-vindas da JM Consultoria e solicita o consentimento de tratamento de dados conforme a LGPD com botões "Concordo e Continuar" e "Saber Mais".
- **AC-01-2:** Dado que o usuário clica em "Concordo e Continuar", quando a confirmação é registrada, então o sistema armazena a data/hora, número de WhatsApp e IP/identificador do consentimento e solicita o CPF do cliente para consulta de triagem.
- **AC-01-3:** Dado que o usuário digita um CPF no chat, quando o sistema realiza a validação do dígito verificador, então se o CPF for matematicamente inválido, o sistema retorna uma mensagem amigável solicitando a conferência dos números sem travar a sessão.
- **AC-01-4:** Dado que um CPF válido é recebido com consentimento, quando o motor de triagem consulta a elegibilidade e margem consignável preliminar, então o sistema classifica o proponente (ex: Aposentado/Pensionista INSS, Servidor, Trabalhador CLT com saldo FGTS) e apresenta o menu de produtos correspondentes.
- **AC-01-5:** Dado que o usuário digita "falar com atendente" ou o bot não compreende 2 entradas consecutivas, quando o gatilho de transbordo é acionado, então o sistema pausa o fluxo automático, marca a conversa como "Aguardando Operador" no painel da JM Consultoria e notifica o usuário de que um consultor assumirá o chat.

### E02 — Motor de Simulação Multibancos e Apresentação de Propostas

- **AC-02-1:** Dado que o cliente selecionou o produto desejado (ex: Consignado INSS ou FGTS), quando o sistema envia requisição para as APIs dos bancos parceiros homologados, então compila as simulações retornadas em até 3 segundos contendo valor liberado, quantidade de parcelas, valor da parcela, taxa de juros nominal e CET.
- **AC-02-2:** Dado que múltiplas propostas foram geradas com sucesso, quando o sistema formata a resposta no WhatsApp, então exibe as propostas ordenadas da menor taxa/maior benefício para a maior, destacando a "Opção Recomendada" de forma visualmente limpa e legível em tela de smartphone.
- **AC-02-3:** Dado que o cliente deseja personalizar prazos ou valores diferentes dos sugeridos, quando ele clica no botão "Outros Valores/Prazos", então o bot oferece opções de ajuste de prazo (ex: 24x, 36x, 48x, 84x) e recalcula as propostas em tempo real.
- **AC-02-4:** Dado que o cliente clica no botão "Escolher Esta Proposta", quando a escolha é registrada, então o sistema congela as condições simuladas por 15 minutos (reserva de tabela) e gera o identificador único da proposta (`proposal_id`).

### E03 — Coleta, Validação Cadastral e Documentoscopia (OCR)

- **AC-03-1:** Dado que o cliente confirmou a proposta, quando o bot solicita os dados bancários para recebimento do crédito, então valida se o banco, agência e conta informados (ou chave PIX) são de titularidade do mesmo CPF do proponente.
- **AC-03-2:** Dado que a conta bancária é informada com titularidade divergente (CPF diferente), quando o sistema valida os dados cadastrais, então alerta imediatamente o cliente no chat que as normas do BACEN proíbem pagamento de crédito consignado em contas de terceiros e solicita uma conta no próprio nome.
- **AC-03-3:** Dado que o bot solicita a foto do documento de identificação (RG ou CNH), quando o cliente envia a imagem pelo WhatsApp, então o serviço de OCR extrai os campos Nome, CPF, Data de Nascimento e Órgão Emissor em até 4 segundos.
- **AC-03-4:** Dado que a foto enviada pelo cliente está borrada, cortada ou com reflexos que impedem a leitura pelo OCR, quando a taxa de confiança do OCR for inferior a 70%, então o bot envia uma mensagem orientando como tirar uma foto nítida e solicita um novo envio.
- **AC-03-5:** Dado que os dados do documento foram extraídos com sucesso e conferem com os dados digitados na simulação, quando a checagem antifraude preliminar (status do CPF na Receita Federal e ausência de bloqueios cadastrais) retorna positiva, então a proposta avança automaticamente para o status `ready_for_formalization`.

### E04 — Formalização Digital, Biometria Facial e Assinatura da CCB

- **AC-04-1:** Dado que a proposta está aprovada para formalização, quando o sistema aciona a esteira do banco parceiro, então gera o link único e criptografado da Cédula de Crédito Bancário (CCB) e o envia no WhatsApp do cliente com prazo de validade de 24 horas.
- **AC-04-2:** Dado que o cliente abre o link de formalização no navegador do celular, quando a página é carregada, então exibe o resumo completo do contrato (valor financiado, taxas, parcelas, valor líquido a receber e dados da conta de crédito) de forma clara antes do aceite.
- **AC-04-3:** Dado que o cliente avança para a etapa de prova de vida, quando a câmera do celular é ativada, então o motor biométrico realiza teste de liveness (liveness passivo/ativo) e faz o matching facial contra o documento oficial com índice de similaridade dentro da margem de segurança.
- **AC-04-4:** Dado que a biometria facial foi concluída e o cliente clica em "Assinar Contrato", quando a assinatura digital com carimbo de tempo e certificado ICP-Brasil/validade jurídica é gravada, então o status da proposta é atualizado para `signed_and_formalized` e o cliente recebe mensagem de confirmação instantânea no WhatsApp.
- **AC-04-5:** Dado que o cliente não concluiu a formalização após 2 horas do envio do link, quando o monitor de pendências identifica o abandono, então envia uma notificação amigável de lembrete pelo WhatsApp com botão de reabertura do link seguro.

### E05 — Averbação, Desembolso Financeiro e Notificação em Tempo Real

- **AC-05-1:** Dado que o contrato foi formalizado com sucesso, quando o sistema transmite a proposta para a esteira do banco parceiro, então atualiza o status para `in_averbation` e notifica o cliente no WhatsApp de que o contrato está em fase de averbação junto ao órgão pagador (ex: Dataprev).
- **AC-05-2:** Dado que a averbação é recusada pelo órgão (por exemplo, por margem insuficiente ou benefício bloqueado para empréstimo), quando o webhook bancário devolve o motivo da recusa, então o sistema registra o log, envia mensagem esclarecedora ao cliente com a orientação de regularização e encaminha o caso com alerta de alta prioridade para o operador da JM Consultoria.
- **AC-05-3:** Dado que o contrato é averbado com sucesso, quando o banco parceiro realiza a ordem de pagamento (PIX ou TED), então o sistema recebe a confirmação via webhook em menos de 30 segundos.
- **AC-05-4:** Dado que o pagamento foi confirmado pelo banco, quando o evento de liquidação é processado, então o sistema envia imediatamente pelo WhatsApp uma mensagem parabenizando o cliente, confirmando que o valor já foi creditado e disponibilizando o comprovante da operação e a cópia da CCB para download.
- **AC-05-5:** Dado que a proposta foi finalizada e paga, quando o ciclo se encerra, então o sistema dispara uma pesquisa NPS conversacional rápida de 1 clique no WhatsApp ("De 0 a 10, como você avalia sua experiência?") e registra a métrica no painel analítico.

---

## Constraints
- **Regulatórias:** Cumprimento da Resolução CMN 3.954/2011, Resolução CMN 4.935/2021 (contratação eletrônica de operações de crédito) e Lei nº 13.709/2018 (LGPD).
- **Arquitetura de Mensageria:** Uso de WhatsApp Business Cloud API com webhooks assíncronos e idempotentes para evitar envio duplicado de mensagens ou processamento repetido de transações.
- **Segurança de Dados:** Armazenamento seguro com chaves gerenciadas de todas as informações sensíveis (PII, imagens de CNH/RG e dados de pagamento).

## Assumptions
- **Assumption:** A taxa média de disponibilidade das APIs de simulação dos bancos parceiros é ≥ 99% em dias úteis. *(Verificação: testar SLA com a promotora parceira no onboarding).*
- **Assumption:** O tempo de liquidação via PIX pelo banco parceiro ocorre em até 30 minutos após averbação concluída. *(Verificação: homologar esteira no ambiente de testes).*

## Dependencies
- Credenciamento oficial e chaves de API/Sandbox fornecidas pelas promotoras ou bancos conveniados até a data de início da sprint de integração.
- Conta Meta Business Manager verificada e número de telefone homologado no WhatsApp Cloud API.

## NFR Pointer
- Conforme diretrizes técnicas: latência p95 das mensagens do bot ≤ 1,8s; criptografia TLS 1.3 em trânsito; retenção de dados cadastrais conforme prazo regulatório do BACEN (5 anos) com auditoria de logs.

## Open questions
- [ ] **(importante)** O gateway de biometria será o nativo do banco parceiro (redirecionamento) ou contratado à parte (ex: Unico / idwall)? — *owner: Jéssica Angie*
- [ ] **(importante)** A esteira deve priorizar banco com maior comissão ou banco com menor taxa para o cliente no ranking das propostas? — *owner: Jéssica Angie*

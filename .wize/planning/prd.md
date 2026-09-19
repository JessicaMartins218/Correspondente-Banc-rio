---
status: ready-for-solutioning
owner: Maria Hill
created: 2026-09-19
---

# PRD — Correspondente Bancário Autônomo via WhatsApp

## Goals
1. **Volume de Conversão Diária:** Alcançar e sustentar a conversão mínima de 15 contratos pagos por dia (10 contratos para FGTS e Consignado CLT; 5 contratos para Consignado INSS) no prazo de 60 dias após implantação do MVP (métrica: `daily_paid_contracts_count`, meta: ≥ 15/dia).
2. **Autonomia Operacional de Atendimento:** Atingir índice de resolução automatizada de ponta a ponta ≥ 75%, desde o primeiro contato do cliente até o envio do link de formalização gerado pelo banco, reduzindo o transbordo manual para no máximo 25% dos atendimentos (métrica: `bot_end_to_end_containment`, meta: ≥ 75%).
3. **Agilidade no Fluxo de Digitação e Formalização:** Reduzir o tempo total entre a confirmação da simulação pelo cliente e a entrega do link de formalização oficial do banco no WhatsApp para ≤ 3 minutos (métrica: `median_time_to_formalization_link`, meta: ≤ 180 segundos).
4. **Resiliência e Proteção do Canal WhatsApp:** Garantir 0 ocorrências de suspensão ou banimento de número no WhatsApp na execução de disparos ativos para bases de contatos, utilizando cadência gradual, aquecimento e rotatividade de cópias (métrica: `whatsapp_number_ban_count`, meta: 0).
5. **Acurácia Cadastral e Segurança de Acesso:** Garantir 100% de precisão na digitação dos dados nos portais bancários e zero vazamentos de credenciais de login ou dados bancários dos proponentes (métrica: `typing_accuracy_rate`, meta: 100%; `security_incident_count`, meta: 0).

---

## Scope

### In scope
- **Conexão e Gestão de Mensageria WhatsApp:** Recepção de mensagens de clientes (receptivo de indicações) e motor de disparo ativo de prospecção (outbound) para bases de contatos com fila e cadência anti-banimento.
- **Acolhimento e Consentimento LGPD:** Apresentação da JM Consultoria, registro explícito e auditável do consentimento de privacidade conforme Lei nº 13.709/2018 e validação de CPF.
- **Motor de Automação de Navegador (RPA Bancário):** Módulo headless (Playwright/Puppeteer) capaz de autenticar com login e senha nos portais web dos bancos parceiros homologados (Banco DSV e Banco Prata).
- **Simulação Automatizada nos Bancos:** Execução de simulações em tempo real nos portais bancários para os produtos Saque-Aniversário FGTS, Consignado CLT e Consignado INSS (margem nova, refinanciamento e portabilidade).
- **Apresentação e Seleção de Propostas:** Formatação amigável e comparativa das condições simuladas (valor líquido liberado, parcelas, prazo, taxa de juros e CET) diretamente no chat do WhatsApp para escolha do cliente.
- **Coleta Cadastral e Validação de Conta:** Coleta de dados complementares do proponente e checagem de titularidade obrigatória da conta bancária de recebimento (mesmo CPF do titular).
- **Digitação 100% Autônoma da Proposta:** Preenchimento automatizado de todos os campos no portal do banco pelo robô via RPA, gerando o contrato na esteira da instituição financeira.
- **Captura e Envio do Link de Formalização Oficial:** Extração do link de formalização digital (biometria facial e assinatura de CCB) gerado pelo portal do banco e envio instantâneo para o WhatsApp do cliente.
- **Acompanhamento de Status e Pós-Venda:** Monitoramento periódico do status da proposta no portal bancário, envio de avisos de averbação/pagamento no WhatsApp, pesquisa NPS de satisfação e régua de relacionamento pós-venda.
- **Transbordo Humano de Exceções:** Notificação imediata para Jéssica Angie ou consultores da JM Consultoria quando o cliente solicitar falar com atendente ou em caso de pendências não resolvidas pelo robô.

### Out of scope
- Atuação como instituição financeira direta ou assunção de risco de crédito (a JM Consultoria atua exclusivamente como Correspondente Bancário no País autorizado).
- Desenvolvimento de aplicativo móvel nativo (iOS/Android) — toda a experiência do tomador é concentrada no WhatsApp e na página web do banco.
- Motor proprietário de biometria facial ou assinatura de CCB (a formalização é 100% realizada na infraestrutura oficial do próprio banco através do link gerado).
- Atendimento via canais secundários (Instagram Direct, Telegram, SMS) no lançamento do MVP (foco exclusivo em WhatsApp).

---

## Backbone (Coarse Stories)

- **E01:** Como cliente ou lead, quero interagir no WhatsApp com atendimento humanizado e segurança LGPD, para que eu possa verificar opções de crédito sem burocracia.
- **E02:** Como cliente interessado, quero receber simulações reais dos bancos parceiros (DSV, Prata) de forma transparente no WhatsApp, para que eu possa escolher a melhor proposta.
- **E03:** Como cliente que escolheu uma proposta, quero fornecer meus dados no chat para que a proposta seja digitada de forma autônoma no portal do banco sem eu ter que esperar um atendente.
- **E04:** Como cliente com proposta digitada no banco, quero receber o link oficial de formalização direto no WhatsApp, para que eu assine e realize a biometria facial com comodidade no meu celular.
- **E05:** Como cliente formalizado, quero ser notificado no WhatsApp sobre o andamento da averbação e o momento em que o dinheiro cair na minha conta, contando com suporte no pós-venda.

---

## Acceptance Criteria

### E01 — Atendimento Receptivo, Prospecção Ativa e Triagem LGPD

- **AC-01-1:** Dado que um novo contato envia uma mensagem para o WhatsApp do robô, quando o webhook processa a entrada em até 1,5 segundo, então envia uma saudação acolhedora da JM Consultoria e apresenta o termo de consentimento LGPD com opção de concordar para prosseguir.
- **AC-01-2:** Dado que o cliente confirma o aceite dos termos LGPD, quando o sistema registra o log de consentimento (data/hora UTC, telefone e identificador único), então solicita o número do CPF do proponente para validação.
- **AC-01-3:** Dado que o cliente envia seu CPF no chat, quando o validador algorítmico verifica os dígitos verificadores, então se o CPF for inválido, emite mensagem amigável solicitando a conferência e redigitação dos 11 dígitos; se válido, avança para a escolha do produto.
- **AC-01-4:** Dado que o operador carrega uma base de contatos para prospecção ativa, quando o motor de disparos processa a fila de mensagens, então dispara mensagens personalizadas respeitando um intervalo aleatório entre 15 e 45 segundos por disparo para prevenir bloqueios de número.
- **AC-01-5:** Dado que o cliente digita comandos como "falar com atendente", "humano" ou o robô detecta frustração/dúvida não mapeada por 2 vezes seguidas, quando o gatilho de transbordo é ativado, então a automação é pausada na conversa e um alerta com o resumo do lead é enviado para a equipe humana da JM Consultoria.

### E02 — Motor de Automação Web (RPA) para Login e Simulação nos Portais Bancários

- **AC-02-1:** Dado que as credenciais de acesso aos portais dos bancos DSV e Prata estão cadastradas nas variáveis de ambiente seguras, quando o motor de RPA inicializa o navegador headless, então realiza o login no portal do banco com sucesso e mantém o token/sessão ativa para requisições.
- **AC-02-2:** Dado que a sessão do portal bancário expirou por inatividade, quando uma nova requisição de simulação é disparada, então o robô executa a reconexão automática e refaz o login sem falhar a solicitação do cliente.
- **AC-02-3:** Dado que o cliente selecionou o produto (ex: Saque-Aniversário FGTS, Consignado CLT ou INSS) e informou os parâmetros básicos no WhatsApp, quando o robô preenche a tela de simulação do portal bancário, então extrai os valores disponíveis, prazos, valor de parcela, taxas nominais e CET em até 15 segundos.
- **AC-02-4:** Dado que os dados da simulação foram obtidos dos portais parceiros, quando a mensagem de retorno é construída, então o WhatsApp apresenta as propostas de maneira clara, destacando o valor líquido liberado na conta do cliente e a quantidade/valor das parcelas.
- **AC-02-5:** Dado que o cliente clica ou digita que deseja escolher uma determinada condição simulada, quando a confirmação é recebida, então o sistema vincula os parâmetros escolhidos à sessão da proposta e avança para a etapa de coleta de dados cadastrais.

### E03 — Coleta Cadastral e Digitação Automatizada da Proposta no Portal do Banco

- **AC-03-1:** Dado que a proposta foi confirmada pelo cliente, quando o robô inicia a coleta cadastral no WhatsApp, então solicita os dados complementares exigidos pelo banco (RG/Órgão emissor, data de nascimento, endereço, nome da mãe e dados da conta bancária para crédito).
- **AC-03-2:** Dado que o cliente informa os dados bancários para recebimento (banco, agência, conta ou chave PIX), quando o sistema valida os dados cadastrais, então rejeita chaves ou contas em nome de terceiros e orienta que a conta deve ser obrigatoriamente vinculada ao mesmo CPF do titular do empréstimo.
- **AC-03-3:** Dado que todos os campos obrigatórios foram fornecidos e validados, quando o robô navega até o formulário de digitação de proposta no portal web do banco parceiro, então preenche autonomamente todos os campos e submete a proposta na esteira do banco.
- **AC-03-4:** Dado que o portal bancário acusa uma pendência impeditiva durante a digitação (ex: margem zerada, benefício bloqueado para empréstimo no INSS ou divergência cadastral na Receita), quando o robô captura o erro da tela, então traduz a mensagem técnica para uma explicação clara ao cliente no WhatsApp e abre chamado interno para a JM Consultoria.
- **AC-03-5:** Dado que a digitação é aceita com sucesso pelo portal do banco parceiro, quando a tela de confirmação é renderizada, então o robô captura o número oficial da proposta (`proposal_id`) no banco e salva no histórico do lead.

### E04 — Captura do Link de Formalização do Banco e Condução da Assinatura no WhatsApp

- **AC-04-1:** Dado que a proposta foi submetida com sucesso no portal bancário, quando o portal gera a URL oficial de formalização/assinatura eletrônica, então o robô extrai o link diretamente da página do banco em menos de 5 segundos.
- **AC-04-2:** Dado que o link de formalização foi capturado, quando o sistema formata a mensagem no WhatsApp, então envia o link ao cliente acompanhado de orientações didáticas passo a passo (preparar documento original, estar em ambiente iluminado para a biometria facial e ler o resumo do contrato).
- **AC-04-3:** Dado que o link de formalização foi enviado, quando o cliente clica no link e realiza a formalização no ambiente seguro do banco, então o status da proposta na base local é atualizado para `awaiting_bank_signature_validation`.
- **AC-04-4:** Dado que se passaram 2 horas desde o envio do link de formalização e a assinatura ainda não consta concluída no portal do banco, quando o monitor de pendências identifica a ausência de formalização, então dispara um lembrete gentil no WhatsApp com o botão de reabertura do link para resgatar a conversão.
- **AC-04-5:** Dado que o link de formalização do banco expira (após 24 horas), quando o cliente tenta retomar o contato, então o robô verifica no portal do banco a possibilidade de reemissão do link ou solicita a revalidação da simulação.

### E05 — Acompanhamento de Esteira, Confirmação de Liquidação e Pós-Venda

- **AC-05-1:** Dado que uma proposta formalizada está em averbação no banco parceiro, quando o motor de consulta verifica periodicamente o portal do banco (via rotina agendada), então captura a mudança de status e atualiza a esteira interna.
- **AC-05-2:** Dado que o contrato é averbado e o banco emite a ordem de pagamento (PIX ou TED), quando o sistema detecta o status de "Contrato Pago/Liquidado" no portal, então envia imediatamente uma mensagem comemorativa no WhatsApp do cliente informando que o dinheiro já está na conta informada.
- **AC-05-3:** Dado que o pagamento foi confirmado, quando a jornada principal se encerra, então o robô envia uma pesquisa rápida de satisfação (NPS de 1 a 5 estrelas ou 0 a 10) diretamente na conversa para medir a qualidade do atendimento.
- **AC-05-4:** Dado que se completam 30, 60 e 90 dias após a contratação, quando a régua de pós-venda é acionada, então envia mensagens de relacionamento e ofertas de refinanciamento, portabilidade ou novo saque FGTS se houver margem disponível recalculada.
- **AC-05-5:** Dado o encerramento de cada dia útil, quando a rotina de consolidação executa, então gera um relatório diário para Jéssica Angie contendo o total de contratos pagos no dia (comparando com a meta de 15/dia: 10 FGTS/CLT e 5 INSS), taxa de conversão e volume financeiro originado.

---

## Constraints
- **Automação RPA:** Os bancos iniciais (DSV e Prata) não dispõem de API REST para correspondentes; a automação depende da estabilidade do DOM/HTML dos portais web. Scripts de RPA devem ter seletores resilientes e timeouts configuráveis.
- **Segurança de Credenciais:** As credenciais de acesso aos portais bancários devem ser armazenadas exclusivamente em variáveis de ambiente protegidas (`.env`) ou cofre de segredos, nunca expostas no código-fonte ou em logs.
- **Políticas da Meta / WhatsApp:** Respeito integral às diretrizes de mensagens da Meta para evitar denúncias de spam e bloqueio do número comercial da JM Consultoria.
- **Compliance Bancário e LGPD:** Vedação estrita de crédito em contas bancárias de terceiros (norma BACEN). Conformidade com a guarda segura de dados cadastrais por 5 anos conforme exigência regulatória.

## Assumptions
- O portal dos bancos parceiros permanece acessível em horário comercial com tempo de resposta estável para carregamento das telas de simulação e digitação.
- Os bancos parceiros geram o link de formalização digital imediatamente após a submissão da proposta na web.
- O WhatsApp Business da JM Consultoria será integrado através de um gateway compatível com webhooks (ex: Evolution API ou Z-API).

## Dependencies
- Credenciais válidas e ativas para acesso aos portais web dos bancos DSV e Prata.
- Instância de gateway do WhatsApp conectada com o número da JM Consultoria.
- Ambiente com suporte à execução de navegadores headless (Node.js + Playwright/Puppeteer).

## NFR Pointer
- Latência de resposta do bot no WhatsApp: p95 ≤ 2 segundos para mensagens de conversa direta.
- Tempo de execução de simulação via RPA: ≤ 15 segundos por banco.
- Tempo de digitação e geração do link de formalização no portal: ≤ 60 segundos.
- Disponibilidade do serviço: 99,5% em horário comercial (08h às 20h).

## Open questions
- [ ] **(importante)** Definição da ferramenta de gateway de WhatsApp: Evolution API (hospedada em servidor próprio) ou Z-API (SaaS)? — *owner: Jéssica Angie*
- [ ] **(importante)** Criação de usuário secundário nos portais DSV e Prata para o robô ou uso das credenciais principais da Jéssica? — *owner: Jéssica Angie*
- [ ] **(nice-to-know)** Mapeamento dos portais e produtos dos novos bancos a serem homologados nesta semana. — *owner: Jéssica Angie*

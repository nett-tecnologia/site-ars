# Checklist para SaaS desenvolvido com IA: produto, privacidade e conformidade

Versão: 27/10/2026 | Produto/repositório: ______ | Responsável: ______ | Mercado: ______ | Revisão: ______

## Aplicação

Use com `CHECKLIST_SEGURANCA_SAAS.md` antes da publicação e em mudanças relevantes. O fato de o software ter sido criado com IA não altera, por si só, todas as obrigações; avalie o funcionamento real, público, dados, contratos e jurisdições. Preencha status, responsável, evidência e prazo. P0 = condição crítica para lançamento, P1 = antes da exposição ampliada, P2 = melhoria planejada. Revise com jurídico e especialistas conforme o produto. Nenhum checklist impede processos ou garante conformidade.

Ficha: empresa/controlador ___; operador(es) ___; SaaS ___; dados e titulares ___; finalidade ___; clientes e países ___; fornecedor de IA ___; dados de saúde/crianças? ___; retenção ___; contato de privacidade ___; versão ___; data ___; responsável ___; próxima revisão ___. Não inclua dados pessoais reais ou segredos como evidência em repositório público.

## 1. Os 20 itens dos prints: o que verificar

- [ ] **1. Política de privacidade — P0:** publicada, acessível e fiel às operações: responsável e contato, dados, finalidades, bases legais pertinentes, compartilhamentos, transferências, retenção e direitos. Atualizar quando mudar o tratamento. Evidência: versão e comparação com fluxos reais.
- [ ] **2. Termos de uso — P0:** regras de acesso, contratação, funções, responsabilidades, suporte, disponibilidade, suspensão, encerramento e condições financeiras quando aplicáveis; versão, aceite comprovável quando necessário e revisão jurídica. Termos não afastam direitos legais.
- [ ] **3. Cookies — P0 quando aplicável:** inventariar cookies, SDKs e tecnologias similares por finalidade; avaliar base legal, normas locais e necessidade de consentimento. Quando necessário, oferecer recusa tão fácil quanto aceite, escolha granular, revogação e bloqueio prévio dos não essenciais; testar na rede. Banner genérico não resolve sozinho.
- [ ] **4. Formulários e LGPD — P0:** informar finalidade, campos necessários, contato e aviso de privacidade; definir base legal adequada antes da coleta. Consentimento não é a única base e não deve ser presumido nem condicionado indevidamente. Validar no servidor e restringir acesso.
- [ ] **5. Reembolso — P0 quando aplicável:** condições claras de cobrança, cancelamento e reembolso, coerentes com oferta, contrato e lei. Avaliar CDC e direito de arrependimento quando aplicável a contratação de consumo fora do estabelecimento; não presumir que todo contrato B2B tem as mesmas regras. Testar processo real.
- [ ] **6. Coleta mínima — P0:** mapear cada campo e justificar necessidade, finalidade, acesso e prazo; remover dados sem propósito. Não coletar dados sensíveis para demonstração ou testes.
- [ ] **7. Exclusão — P0:** procedimento para solicitações do titular, confirmação de identidade, avaliação legal e execução em bancos, terceiros e backups conforme retenção e viabilidade; registrar resposta, prazo e exceções. Exclusão não é automática nem absoluta: certas retenções legais podem se aplicar.
- [ ] **8. Google Analytics — P1 se usado:** documentar identificadores, dados, configuração, localização e termos do fornecedor; revisar transferências e base legal, e condicionar disparo quando necessário. Testar coleta real e não enviar dados pessoais em URLs ou eventos.
- [ ] **9. Scripts de rastreamento — P1 se usados:** inventariar pixels, tags, SDKs, finalidade, responsável, compartilhamento e base legal; remover scripts não necessários; validar se carregam apenas após escolha exigida e se revogação funciona.
- [ ] **10. Terceiros — P0:** inventariar hospedagem, pagamentos, IA, e-mail, suporte e analytics; avaliar segurança, contrato, papéis, subprocessadores, região, retenção, notificações e transferências internacionais. Registrar fornecedor e responsável por revisão.
- [ ] **11. Acessibilidade — P1:** adotar WCAG 2.2 AA como meta técnica, avaliar obrigações aplicáveis e testar jornadas com ferramentas automáticas e testes humanos, inclusive leitor de tela. Documentar falhas e correções; automação não cobre tudo.
- [ ] **12. Textos alternativos — P1:** imagens informativas têm descrição útil no contexto; imagens decorativas não geram ruído; ícones funcionais possuem nome acessível.
- [ ] **13. Contraste — P1:** verificar texto, estados, foco e componentes segundo critérios WCAG pertinentes; não transmitir informação apenas pela cor.
- [ ] **14. Teclado — P1:** percorrer todas as jornadas com teclado, foco visível e ordem lógica; sem armadilhas; testar menus, diálogos e formulários.
- [ ] **15. Botões claros — P1:** nome acessível e ação explícita, mensagens de erro compreensíveis, rótulos e instruções; confirmação para ações destrutivas e atenção a acessibilidade de autenticação.
- [ ] **16. Depoimentos — P0 se publicados:** reais, autorizados, identificados de forma adequada e comprováveis; não fabricar avaliações ou apresentar conteúdo gerado como relato real. Respeitar privacidade.
- [ ] **17. Promessas — P0:** evidenciar alegações de desempenho, disponibilidade, certificações e segurança; evitar garantia absoluta ou certificação inexistente. Registro de software não equivale a patente. Aprovar material comercial.
- [ ] **18. Direitos de imagens — P0:** verificar licença, uso comercial, atribuição, direitos de personalidade e condições das ferramentas de geração; guardar comprovantes, sem supor que toda imagem da internet é livre.
- [ ] **19. Dados da empresa — P0:** identificação do fornecedor, canais e informações exigidas no contexto de oferta/contratação; verificar CNPJ, endereço e atendimento de acordo com o serviço e legislação aplicável.
- [ ] **20. Leis aplicáveis — P0:** identificar países onde o serviço é ofertado, titulares, dados e contratos; avaliar LGPD, CDC e normas setoriais; GDPR/UK GDPR ou outras regras quando houver vínculo aplicável. Cláusula de foro ou lei escolhida não elimina normas obrigatórias.

## 2. Governança de dados

- [ ] **P0:** mapear ciclo de vida: coleta, armazenamento, acesso, compartilhamento, retenção e descarte; documentar controlador/operador por operação, finalidade e base legal (inclusive regra própria para dados sensíveis).
- [ ] **P1:** manter registro das operações, política de retenção e procedimento de atendimento dos direitos; avaliar necessidade de encarregado, relatório de impacto e medidas específicas conforme lei e risco.
- [ ] **P0:** avaliar dados de saúde, crianças e outras categorias sensíveis; coletar somente o necessário, restringir acesso, registrar visualizações críticas e verificar legislação profissional e setorial. Para Instituto Terapia, revisar prontuários, sigilo, teleatendimento e regras dos conselhos profissionais antes de operar.
- [ ] **P1:** avaliar transferência internacional real, inclusive suporte, backups, telemetria e IA; revisar mecanismo legal e contratos. A localização do banco não comprova sozinha residência integral dos dados.
- [ ] **P1:** definir canal de suporte e privacidade com responsável, horário e fluxo de escalonamento; comprovar atendimento e resposta a solicitações.

## 3. Uso responsável de IA

- [ ] **P0:** identificar se IA apenas ajudou a desenvolver o código ou se trata dados dos usuários em produção; documentar funcionalidades, fornecedor, finalidade e limitações reais.
- [ ] **P0:** proibir uso de dados reais sensíveis ou segredos em ferramentas de desenvolvimento sem autorização e base adequada; usar dados fictícios e revisar termos de retenção e treinamento.
- [ ] **P0:** decisões com impacto significativo recebem avaliação jurídica, transparência adequada e revisão humana conforme contexto; IA não substitui profissional responsável. Testar saídas incorretas, vieses, falhas e possibilidade de contestação.
- [ ] **P1:** revisar propriedade, licenças e originalidade de código, conteúdo e dependências gerados; equipe humana valida implementação, acessibilidade, segurança e promessas comerciais.
- [ ] **P1:** quando IA gerar conteúdo para usuário, explicar limitações e permitir correção; validar fontes e não prometer precisão absoluta. Aplicar controles técnicos de IA no checklist de segurança.

## 4. Contratação e operação

- [ ] **P1:** descrever preço, periodicidade, renovação, impostos pertinentes, cancelamento e canal de suporte antes da contratação; testar cobrança, cancelamento e comprovantes.
- [ ] **P1:** alinhar contrato de tratamento de dados com clientes empresariais ou órgãos públicos, responsabilidades de incidente, suboperadores, retenção, exclusão e requisitos do edital.
- [ ] **P1:** registrar política de acessibilidade, canal de solicitação, responsáveis, correções pendentes e data de reavaliação.
- [ ] **P1:** avaliar requisitos contratuais para SLA, residência, disponibilidade, continuidade, backups, portabilidade e saída do cliente; não prometer capacidades ainda não testadas.

## 5. Roteiro de auditoria reutilizável

1. Preencher a ficha e inventariar telas, formulários, cookies, dados, integrações, países e provedores.
2. Aplicar os 20 itens e os controles adicionais; apontar N/A com justificativa e evidência.
3. Examinar o comportamento em produção: testar coleta, consentimento quando exigido, acesso, exclusão, cancelamento e acessibilidade.
4. Fechar P0; registrar P1, prazos, responsáveis, decisões e revisão jurídica quando necessária.
5. Guardar evidências protegidas e revisar em alterações de produto, fornecedor, mercado, incidente e periodicamente.

Registro: ID ___ | item ___ | aplicabilidade ___ | status ___ | evidência ___ | responsável ___ | prazo ___ | decisão ___ | reteste ___ | revisão ___.

## Fontes de referência

- [LGPD — Lei 13.709/2018](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)
- [ANPD — guias e orientações](https://www.gov.br/anpd/pt-br/documentos-e-publicacoes)
- [Decreto 7.962/2013 — comércio eletrônico](https://www.planalto.gov.br/ccivil_03/_ato2011-2014/2013/decreto/d7962.htm)
- [WCAG 2.2 — W3C](https://www.w3.org/TR/WCAG22/)
- [OWASP LLM Verification Standard](https://owasp.org/www-project-llm-verification-standard/LLMSVS-v2.0-en.html)

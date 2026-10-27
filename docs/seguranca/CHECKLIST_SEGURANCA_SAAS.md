# Checklist de segurança técnica e proteção de dados para SaaS

Versão: 27/10/2026 | Repositório: ______ | Ambiente: ______ | Responsável: ______ | Revisão: ______

## Como usar

Copie os dois checklists para `docs/seguranca/` em cada repositório. Para cada item registre **status** (pendente, em andamento, aprovado ou não aplicável), responsável, prazo e evidência (arquivo, teste, configuração ou link). Não marque como aprovado apenas porque o código existe: valide também a configuração efetiva em produção. Não inclua segredos, dados pessoais reais nem evidências sensíveis no repositório.

**P0** bloqueia a publicação até correção ou decisão formal documentada; **P1** corrigir antes da exposição ampliada; **P2** melhoria planejada. Estes níveis são uma orientação interna, não uma certificação. O responsável deve avaliar riscos e exigências contratuais específicas. Uma aceitação de risco deve ter justificativa, responsável, medidas compensatórias, prazo e data de revisão; falhas que exponham dados, credenciais ou controle de contas não devem ser aceitas para lançamento sem correção.

Ficha: produto ___; domínio ___; dados e categorias ___; clientes/tenants ___; países ___; serviços ___; responsável técnico ___; contato de incidentes ___; última revisão ___; próximo ciclo ___.

## 1. Segredos e repositório

- [ ] **P0 — Chaves de API:** segredos ficam em gerenciador apropriado, com acesso mínimo por serviço e ambiente; nenhuma chave privada é entregue ao navegador ou embutida no bundle. Chaves públicas identificadas como tais também têm restrições apropriadas. **Evidência:** inventário sem valores, revisão do bundle e configuração.
- [ ] **P0 — `.env`:** arquivos reais ignorados pelo Git, inacessíveis por HTTP e fora de imagens, artefatos e logs; `.env.example` contém apenas exemplos fictícios. Testar URL e histórico.
- [ ] **P0 — Senhas no código:** pesquisar código, scripts, documentação, histórico e CI; usar detecção de segredos em commits/PR. Se houver vazamento, revogar ou rotacionar imediatamente, investigar uso e limpar histórico quando apropriado; apagar o arquivo sozinho não revoga a credencial.
- [ ] **P1:** MFA nas contas Git, nuvem e registrador; acesso mínimo, revisão periódica, branch protegida, revisão de PR e credenciais individuais. Segredos de CI restritos por ambiente; evitar expô-los a PRs não confiáveis.
- [ ] **P1:** inventariar dependências, lockfile, varredura de vulnerabilidades e licenças, atualização com prazo conforme risco e procedência; revisar pacotes sugeridos por IA antes de instalá-los. Gerar SBOM quando relevante.

## 2. Identidade, sessão e autorização

- [ ] **P0 — Login de verdade:** autenticação no servidor ou provedor confiável; não confiar em `localStorage`, estado visual ou rota oculta como prova de identidade. Senhas armazenadas com Argon2id ou algoritmo adequado com salt; nunca em texto puro.
- [ ] **P0 — Permissão no servidor:** validar identidade, perfil, ação e recurso em toda API, função serverless, job e download; negar por padrão. Criar matriz por perfil × ação × recurso.
- [ ] **P0 — Não confiar no ID da tela:** IDs, tenant, papéis e preços recebidos do cliente são dados não confiáveis; carregar vínculo e autorizar cada objeto no servidor. Testar troca de ID, métodos HTTP, buscas, exportações e arquivos.
- [ ] **P0 — Cada um só vê o seu:** isolamento por tenant em consultas, índices, cache, filas, relatórios, backups e storage; testes automatizados entre dois tenants e dois usuários, inclusive criação e alteração. RLS é defesa adicional, não substitui verificar políticas e acesso privilegiado.
- [ ] **P0 — Admin protegido:** MFA obrigatório para administradores, concessão por processo controlado, menor privilégio, reautenticação em ações críticas, registro de auditoria e revisão de acessos. Não criar senha padrão nem endpoint público de bootstrap.
- [ ] **P1:** sessões com cookies `Secure`, `HttpOnly` e `SameSite` apropriado; proteção CSRF para autenticação por cookies; expiração, logout e revogação. Fluxos de recuperação com tokens aleatórios, uso único, prazo curto e mensagens que não enumerem usuários. Testar SSO, convites e troca de senha.
- [ ] **P1 — Limite de tentativas:** limitar login, recuperação, cadastro, APIs caras e upload por conta/IP ou combinação; aplicar limites na infraestrutura compartilhada, proteção contra força bruta e alertas, evitando bloqueio abusivo de contas.

## 3. Banco, infraestrutura e arquivos

- [ ] **P0 — Banco travado:** negar acesso público desnecessário; rede privada ou restrita, TLS, credenciais individuais e privilégios mínimos; separar produção de testes, sem dados reais em ambientes não autorizados. Testar acesso externo e permissões reais.
- [ ] **P0 — Firebase/Supabase/Storage:** validar regras de segurança e RLS para cada tabela/operação e usuário anônimo/autenticado; nunca expor chave privilegiada/service role. Buckets privados por padrão; links assinados de curta duração quando necessários. Testar diretamente pela API, não só pela interface.
- [ ] **P0 — Upload protegido:** autenticar e autorizar, limitar tamanho e quantidade, permitir tipos necessários, conferir conteúdo e extensão, renomear, armazenar fora da raiz executável, impedir path traversal, verificar malware quando aplicável e servir com cabeçalhos seguros. Testar arquivo malicioso, duplo sufixo e download cruzado.
- [ ] **P1:** criptografia em trânsito e repouso conforme risco; inventário e controle das chaves; segredos fora dos logs. Verificar região dos dados, réplicas, backups e fornecedores contra contratos. Brasil exclusivo quando exigido; não presumir que a região do serviço cobre todos os subprocessadores.
- [ ] **P0 — Recuperação:** backups automáticos cifrados, isolados e monitorados; definir RPO/RTO, responsável e retenção. Fazer e registrar restauração em ambiente isolado; testar integridade, permissões e recuperação de dados por tenant.
- [ ] **P1:** infraestrutura como código revisada, inventário, atualizações, contas de serviço separadas, mínimo privilégio, fechamento de portas, alertas e revisão de configurações. Remover recursos e ambientes antigos.

## 4. Código, entradas e navegador

- [ ] **P0 — Validação no servidor:** validar tipo, tamanho, formato, faixa e regras de negócio em todas as entradas, inclusive webhooks e integrações; não aceitar campos extras críticos. Validar assinatura e evitar repetição de webhooks.
- [ ] **P0 — Entrada do usuário:** escapar conforme contexto de saída; sanitizar HTML com biblioteca apropriada quando permitido; proteger contra XSS, SSRF, comandos e path traversal. Nunca assumir que uma limpeza genérica resolve todos os contextos.
- [ ] **P0 — SQL:** consultas parametrizadas/ORM seguro; evitar interpolação e SQL dinâmico inseguro; validar nomes de colunas e ordenação por lista permitida. Testar injeção e permissões do banco.
- [ ] **P0 — Debug e erros:** desativar debug e endpoints de teste em produção; erros públicos genéricos com ID de correlação; detalhes somente em logs protegidos, sem tokens, senha ou dados sensíveis.
- [ ] **P1 — Headers e CORS:** configurar CSP adequada, `X-Content-Type-Options`, proteção contra framing e `Referrer-Policy`; HSTS após confirmar HTTPS integral. CORS com origens e métodos necessários; sem wildcard com credenciais. CORS não substitui autenticação ou autorização.
- [ ] **P1:** proteger operações não idempotentes, fluxos de pagamento e alterações de privilégio contra repetição e concorrência; validar valores no servidor e assinatura do provedor.

## 5. Operação, incidentes e testes

- [ ] **P1:** logs estruturados de autenticação, autorização negada, mudanças administrativas, exportação e ações críticas, com horário e ator; integridade, retenção e acesso limitado. Alertar sobre anomalias sem registrar conteúdo desnecessário.
- [ ] **P1:** monitorar disponibilidade e falhas, definir responsáveis e canal de alerta; testar alertas e procedimentos, não apenas criá-los.
- [ ] **P1:** plano de incidentes: identificar, conter, preservar evidências, avaliar, recuperar, comunicar e revisar; contatos e responsáveis definidos; ensaio registrado. O controlador deve avaliar comunicação à ANPD e titulares quando houver risco ou dano relevante, conforme RCIS e prazos aplicáveis; operador informa controlador conforme contrato. Há regra geral de três dias úteis, sujeita a condições e legislação específica; consultar norma vigente.
- [ ] **P0 — Teste como estranho:** testar sem login, como usuário comum, como outro tenant e como admin; acessar APIs diretamente e tentar modificar IDs, métodos e papéis; testar arquivos, convites, exports e URLs antigas. Registrar resultados e correções.
- [ ] **P1 — Auditoria com IA:** usar IA como apoio para revisão de código e geração de testes, sem enviar segredos ou dados pessoais indevidos; verificar manualmente seus achados, reproduzir, corrigir e retestar. IA não substitui revisão humana, testes de intrusão autorizados nem auditoria independente.
- [ ] **P1:** antes de cada release executar testes de autorização, segredos, dependências e regressão; revisar mudanças de infraestrutura e plano de rollback. Fazer avaliação independente proporcional ao risco antes de exposição relevante.

## 6. IA em desenvolvimento e funcionalidades de IA — quando aplicável

- [ ] **P0:** código gerado é revisado por pessoa responsável; testar autenticação, isolamento, validação e permissões; não aceitar código só porque compila. Revisar licenças e origem de bibliotecas.
- [ ] **P0:** tratar prompts, documentos, resultados de busca, páginas e respostas de ferramentas como conteúdo não confiável; impedir que instruções nesses conteúdos alterem permissões, revelem segredos ou sejam executadas como comandos. Testar injeção direta e indireta.
- [ ] **P0:** ferramentas/agentes têm permissões mínimas, limites de custo e ações; separar leitura e escrita e exigir confirmação humana para ações sensíveis. Não executar código ou SQL gerado sem validação e isolamento.
- [ ] **P1:** avaliar dados enviados ao provedor, finalidade, região, retenção, treinamento, subprocessadores e contrato; minimizar ou anonimizar quando possível. Segregar contexto e recuperação de dados por tenant.
- [ ] **P1:** validar e codificar saídas antes de exibir, salvar ou executar; testar alucinações, vazamento entre clientes, abuso, consumo e falhas do provedor. Monitorar sem registrar prompts sensíveis desnecessariamente.

## 7. Roteiro mínimo de aceite

1. Inventariar ativos e dados; aplicar os dois checklists e marcar itens não aplicáveis com justificativa.
2. Fechar P0, executar testes de acesso cruzado, segredos, backups e recuperação, e registrar evidências.
3. Revisar P1 e riscos com responsável; definir prazos e proteção compensatória.
4. Registrar versão implantada, ambiente, data, responsáveis e decisão de publicação.
5. Repetir a cada release relevante, mudança de fornecedor ou incidente e periodicamente.

Registro de achado: ID ___ | item ___ | risco ___ | evidência segura ___ | responsável ___ | prazo ___ | correção ___ | reteste ___ | status ___ | exceção e validade ___.

## Referências

- [OWASP Top 10:2025](https://owasp.org/Top10/2025/)
- [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)
- [OWASP LLM Verification Standard](https://owasp.org/www-project-llm-verification-standard/LLMSVS-v2.0-en.html)
- [ANPD — comunicação de incidentes](https://www.gov.br/anpd/pt-br/assuntos/comunicacao-de-incidentes-de-seguranca-cis)
- [LGPD — Lei 13.709/2018](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)

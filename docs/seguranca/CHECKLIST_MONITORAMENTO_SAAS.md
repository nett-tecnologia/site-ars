# Checklist de monitoramento e resposta a incidentes para SaaS

Versão 27/10/2026 | Sistema: ____ | Repositório: ____ | Ambiente: ____ | Responsável: ____ | Revisão: ____

Use com `CHECKLIST_SEGURANCA_SAAS.md` e `CHECKLIST_SAAS_IA_PRIVACIDADE.md`. Preencha por sistema e ambiente; identifique dados sensíveis, serviços, responsável principal e substituto, horários de cobertura e contatos. Para cada controle registre status (pendente, implantado, testado ou não aplicável), fonte, evidência, responsável e revisão. Não colocar credenciais, dados de pacientes, tokens ou logs sensíveis no Git.

## Prioridades e operação

- **P0 — crítico:** indisponibilidade total, segredo exposto, acesso indevido confirmado ou exposição de dados. Acionar imediatamente o responsável disponível e executar contenção.
- **P1 — alto:** falha de backup, aumento sustentado de erros, mudança administrativa inesperada ou degradação relevante. Investigar conforme cobertura e impacto.
- **P2 — acompanhamento:** capacidade, custos, vencimentos e tendências; revisar na rotina.
- Estes são exemplos, não prazos contratuais. Definir tempos de resposta por produto, cobertura 8x5 ou 24x7 e canal alternativo. Não prometer cobertura sem equipe designada.

## 1. Inventário e responsáveis

- [ ] Identificar front-end, API, autenticação, banco, filas, storage, domínios, integrações, repositórios, ambientes e provedor de IA quando existir.
- [ ] Registrar URLs e identificadores, região, criticidade, proprietário, substituto, contato, horário de cobertura e dependências.
- [ ] Definir quais dados de monitoramento podem ser acessados, prazo de retenção, locais, classificações e quem pode ver cada alerta.
- [ ] Identificar serviços ainda sem monitoramento; marcar **desconhecido** em vez de saudável.

## 2. Disponibilidade e desempenho

- [ ] **P0:** monitorar site e endpoint de saúde da API de forma independente; alertar após falhas consecutivas para reduzir falsos alarmes. Configurar limiar conforme serviço; ensaiar uma falha controlada.
- [ ] **P1:** acompanhar latência, taxa de erros HTTP, requisições, saturação e falhas por serviço; observar tendência e definir limites após medir comportamento normal.
- [ ] **P1:** monitorar dependências essenciais, login e jornadas críticas com teste sintético seguro e conta de teste quando apropriado. Um HTTP 200 isolado não comprova que o login, o banco ou a jornada funcionam.
- [ ] **P2:** monitorar vencimento de certificados e domínio com antecedência; validar canais e plano de renovação.
- [ ] Saúde pública deve retornar informações mínimas; não expor nomes internos, versão, dados, credenciais nem detalhes de infraestrutura. Dependências privadas exigem teste autenticado ou interno apropriado.

## 3. Segurança e dados

- [ ] **P0:** alertar exposição confirmada de segredos; revogar/rotacionar, verificar uso e investigar; remoção do Git não invalida o segredo.
- [ ] **P0:** detectar exposição pública inesperada de dados, banco ou bucket; restringir acesso, preservar evidências e avaliar impacto.
- [ ] **P1:** monitorar repetidas falhas de login, redefinições suspeitas, logins administrativos anômalos e alterações de permissões; calibrar para não gerar excesso de alertas.
- [ ] **P1:** registrar e revisar ações sensíveis: criação de administrador, alteração de política, exportações em massa e acessos negados entre clientes. Não presumir que logs provam ausência de falhas.
- [ ] **P1:** rastrear mudanças de rede, credenciais, configuração e regras de acesso em nuvem e repositório; proteger e revisar logs de auditoria.
- [ ] **P1:** habilitar alertas de dependências, varredura de segredos e código conforme disponibilidade e plano; classificar e corrigir, não apenas contar alertas.
- [ ] **P1:** limitar logs ao necessário; mascarar dados pessoais e tokens, restringir acesso, definir retenção e proteger integridade. Nunca enviar dados sensíveis completos para painel ou notificações.

## 4. Backups, operação e custos

- [ ] **P0/P1:** acompanhar sucesso, falha e idade do último backup de cada base; configurar alerta se não ocorrer dentro da janela definida.
- [ ] **P1:** agendar teste de restauração isolado e registrar data, resultado, responsável, integridade e tempo; backup bem-sucedido não comprova restauração funcional.
- [ ] **P1:** monitorar armazenamento, conexões, CPU/memória e filas conforme arquitetura; testar alertas de capacidade.
- [ ] **P2:** configurar orçamento e alertas de consumo por projeto/serviço e IA; orçamento alertado não é necessariamente limite de gasto. Investigar picos e definir ações de contenção.
- [ ] **P1:** registrar falhas de deploy, mudanças de versão e possibilidade de rollback. Comparar incidentes com alterações recentes.

## 5. Alertas e resposta

- [ ] Configurar responsável, substituto, canal e escalonamento; testar recebimento e acompanhar falhas de entrega. Definir canal alternativo se o principal ficar indisponível.
- [ ] Para cada alerta registrar: fonte, condição, janela, prioridade, destinatário, ação, link do procedimento, data do último teste e revisão.
- [ ] Ensaiar incidente: detectar → classificar → conter → preservar evidências → avaliar impacto → recuperar → comunicar → revisar. Registrar cronologia e decisões.
- [ ] Avaliar dados pessoais afetados, papéis de controlador e operador, contratos e necessidade de comunicação à ANPD e titulares conforme lei e prazos vigentes. Não publicar detalhes ou dados no painel compartilhado.
- [ ] Após o incidente, revisar causa, impacto, ações corretivas, responsável e prazo; testar se a correção funciona.

## 6. GitHub, GCP e Cloudflare

- [ ] **GitHub:** inventariar repositórios e ambientes; verificar alertas de dependências e de segredos e varredura de código quando disponíveis; proteger branches e definir quem recebe alertas. A disponibilidade dos recursos depende do plano, visibilidade e permissões.
- [ ] **GCP:** configurar verificações de disponibilidade, políticas de alerta e canais; acompanhar serviços, banco, backup, logs de auditoria e orçamento. Confirmar que cada alerta possui fonte e teste; métricas e custos variam conforme recursos e volume.
- [ ] **Cloudflare:** revisar analytics, eventos de segurança, domínio e notificações disponíveis no plano; definir alertas pertinentes e acesso restrito. Confirmar configuração efetiva para cada domínio e serviço.
- [ ] Não depender de GitHub Actions para monitoramento de produção: verificações e alertas devem continuar funcionando mesmo quando o repositório ou pipeline estiver indisponível.

## 7. Painel simples para todos os sistemas

### Tela sugerida

| Sistema | Disponibilidade | Segurança | Backup | Última verificação | Alertas | Responsável |
|---|---|---|---|---|---|---|
| Exemplo fictício | Verde | Amarelo | Verde | 10:30 | 2 | Equipe |

Cada linha abre detalhes: status do site/API, número e prioridade de alertas, data do último backup e último teste de restauração, fonte e links restritos para diagnóstico. Mostrar também incidentes abertos e data da última atualização. Não incluir prontuários, senhas, tokens ou conteúdo de logs.

**Semáforo:** verde = verificações obrigatórias dentro dos critérios e dados recentes; amarelo = alerta não crítico ou degradação; vermelho = falha crítica ou incidente ativo; cinza = fonte ausente, sem permissão, indisponível ou dado vencido. Definir janela de validade por fonte e registrar horário da coleta. Verde significa apenas que as verificações configuradas passaram; não significa que o sistema está seguro.

### Coleta mínima e implantação gradual

1. **Primeira versão:** cadastro dos sistemas, links, responsável e estado manual identificado como manual; status de disponibilidade automático quando houver fonte configurada. Não inventar resultados.
2. **Integração:** backend privado consulta fontes autorizadas do GCP, GitHub e Cloudflare ou recebe eventos autenticados; normaliza status, salva horário e apresenta resumo. Status de backup exige fonte e teste específicos; dados de segurança dependem de recursos habilitados.
3. **Alertas:** manter alertas e notificações na origem; o painel complementa, não substitui o monitoramento ou a resposta. Se integração falhar, mostrar cinza e alertar para perda de telemetria.
4. **Acesso:** painel privado, login e MFA, perfis de leitura/administração, permissões por sistema, TLS, registros de acesso e segredos em servidor ou gerenciador. Nunca inserir token no navegador ou repositório.
5. **Segurança das integrações:** usar credenciais somente leitura e escopo mínimo, separadas por provedor, rotacionadas; validar webhooks, restringir entradas, limitar chamadas e auditar alterações de configuração.
6. **Custos:** verificar preços, planos e limites vigentes antes de habilitar; definir orçamento e começar com poucos sistemas. Alguns alertas e APIs exigem licença ou permissões adicionais.

### Mapeamento por sistema

| Campo | Valor a preencher |
|---|---|
| Sistema e ambiente | ____ |
| Repositório(s) | ____ |
| URL do site e API | ____ |
| Fontes de disponibilidade | ____ |
| Projeto/serviços GCP | ____ |
| Domínio/serviços Cloudflare | ____ |
| Fonte e periodicidade do backup | ____ |
| Alertas de segurança habilitados | ____ |
| Responsável e cobertura | ____ |
| Canais e escalonamento | ____ |
| Último teste de alerta / restauração | ____ |
| Pendências e prazo | ____ |

## Fontes

- [GCP — alertas para verificações de disponibilidade](https://docs.cloud.google.com/monitoring/uptime-checks/uptime-alerting-policies)
- [GCP — visão geral de alertas](https://docs.cloud.google.com/monitoring/alerts)
- [GitHub — configurações de segurança e análise](https://docs.github.com/pt/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-security-and-analysis-settings-for-your-repository)
- [GitHub — auditoria de alertas](https://docs.github.com/en/code-security/concepts/security-at-scale/audit-security-alerts)
- [ANPD — comunicação de incidentes](https://www.gov.br/anpd/pt-br/assuntos/comunicacao-de-incidentes-de-seguranca-cis)

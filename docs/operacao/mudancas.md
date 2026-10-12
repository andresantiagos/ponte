# Processo de mudanças

**Status:** rascunho. Ferramentas e nomes de branch serão ajustados na implantação.

## 1. O que conta como mudança
- Alteração em regra da árvore de decisão (`regras/`).
- Alteração em texto de orientação ou de desfecho.
- Alteração em prompt de modelo ou em instrução de agente.
- Alteração em fluxo do n8n (`fluxos/`).
- Inclusão, troca ou retirada de documento do RAG (`rag/`, `fontes/`).
- Alteração em configuração de canal, limite ou horário.
- Alteração em número de emergência ou em mensagem fixa.

Mudanças de documentação interna não exigem este processo, mas devem ter commit.

## 2. Quem pode propor, quem pode aprovar

| Tipo de mudança | Quem propõe | Quem valida o conteúdo | Quem aprova a entrada em produção |
|---|---|---|---|
| Regra da árvore ou texto de orientação | Equipe técnica | Responsável técnico do CRAS | Responsável técnico do projeto e responsável pela operação |
| Prompt ou instrução de modelo | Equipe técnica | Responsável técnico do projeto | Responsável técnico do projeto |
| Fluxo do n8n ou integração | Equipe técnica | Responsável técnico do projeto | Responsável técnico do projeto |
| RAG (inclusão ou retirada de fonte) | Equipe técnica | Responsável técnico do CRAS, com data da fonte | Responsável técnico do projeto |
| Número de emergência ou mensagem fixa | Não pode ser proposta pela equipe técnica sem validação | Responsável técnico do CRAS e responsável pela operação | Os dois, por escrito |

Ninguém aprova a própria mudança.

## 3. Fluxo de uma mudança

1. **Registro.** Abrir uma entrada no `CHANGELOG.md` com a descrição, a fonte, a data e o motivo.
2. **Branch.** Criar uma branch separada da `main`. Nunca editar a `main` diretamente.
3. **Teste.** Rodar a bateria completa, incluindo `testes/emergencia/`. Mudança só avança com todos os testes passando.
4. **Validação de conteúdo.** Quando a mudança afetar orientação, enviar ao validador indicado na tabela e aguardar resposta por escrito.
5. **Revisão.** Outra pessoa revisa o diff antes da aprovação. Se a equipe for de uma única pessoa, a revisão é feita pelo validador de conteúdo ou por um revisor externo combinado no contrato.
6. **Entrada em produção.** Só após aprovação registrada. Mudança aprovada é publicada com a versão da árvore atualizada.
7. **Monitoramento.** Acompanhar as primeiras 24 horas com verificação manual, conforme o runbook.

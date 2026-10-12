# Runbook: operação do canal de orientação

**Status:** rascunho. Preencher os trechos entre colchetes conforme a infra for implantada.
**Responsável técnico:** [nome]
**Responsável pela operação do serviço:** [Instituto PLUS, nome do responsável]

## 1. Visão geral
Canal de orientação e triagem para gestantes sem renda formal. Componentes: canal de entrada ([WhatsApp/web]), orquestração ([n8n]), árvore de decisão ([versão]), RAG com fontes oficiais datadas, banco de registros de desfecho e painel de acompanhamento.

## 2. Verificação diária (5 minutos)
1. O canal responde a uma mensagem de teste enviada pelo número de monitoramento?
2. O painel mostra atividade nas últimas 24 horas, ou a ausência é justificada?
3. Há alerta aberto de erro ou de emergência não respondida?
4. O último backup concluiu com sucesso?

Se qualquer item falhar, abrir incidente conforme `incidentes.md`.

## 3. Verificação semanal (30 minutos)
1. Rodar a bateria de testes de emergência (`testes/emergencia/`). Todos devem passar.
2. Rodar a bateria de casos fictícios de cada ramo da árvore.
3. Revisar as fontes do RAG e retirar qualquer documento com data vencida ou revogado.
4. Conferir a versão da árvore em produção contra o `CHANGELOG.md`.
5. Revisar a fila de encaminhamento humano: nenhum caso pode estar sem resposta além do prazo definido.

## 4. Desligar o canal (parada de emergência)
Usar quando houver falha em caso de emergência, suspeita de vazamento ou erro grave de orientação.

1. Acionar a parada: [comando ou botão, a definir na implantação].
2. A mensagem fixa passa a ser enviada a todas as entradas: números 192 (SAMU), 180 (violência contra a mulher), 188 (CVV), e o endereço do CRAS de referência.
3. Confirmar com um teste que a mensagem fixa está sendo enviada.
4. Registrar a parada em `logs/` com data, hora, motivo e quem acionou.
5. Comunicar o responsável pela operação do serviço em até [prazo a definir].
6. Não reativar o canal sem autorização do responsável técnico e do responsável pela operação, por escrito.

## 5. Reativar o canal
1. Confirmar que a causa foi identificada e corrigida.
2. Rodar a bateria completa de testes, incluindo emergência.
3. Obter aprovação por escrito dos dois responsáveis.
4. Reativar e monitorar as primeiras 24 horas com verificação manual a cada [intervalo].

## 6. Verificação de disponibilidade
- Se o canal ficar indisponível por mais de [tempo], a mensagem fixa de emergência deve continuar disponível por outro meio (por exemplo, texto publicado no perfil do canal ou no site do Instituto).

## 7. Contatos
| Função | Nome | Contato |
|---|---|---|
| Responsável técnico | [ ] | [ ] |
| Responsável pela operação | [ ] | [ ] |
| Encarregado de dados | [ ] | [ ] |
| Assistente social de referência (CRAS) | [ ] | [ ] |

## 8. Registro
Cada verificação e cada parada gera uma linha em `logs/operacao.log` com data, responsável e resultado. O arquivo `logs/` não é versionado, por conter registros operacionais.

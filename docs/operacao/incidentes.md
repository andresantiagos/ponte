# Procedimento de incidentes

**Status:** rascunho. Prazos marcados como [a definir] devem ser fixados em contrato com o responsável pela operação e com o encarregado de dados.

## 1. Classes de incidente

| Classe | Definição | Exemplos |
|---|---|---|
| **Crítica** | Falha que pode causar dano imediato a uma pessoa, ou vazamento de dados pessoais | Caso de emergência não identificado ou sem resposta; orientação que expõe dados a terceiros; acesso indevido a registros |
| **Alta** | Erro de orientação sobre benefício, ou indisponibilidade prolongada do canal | Regra desatualizada com informação errada; canal fora do ar por mais de [tempo] |
| **Média** | Falha que não gera risco imediato, mas exige correção | Erro de texto; fonte do RAG com data vencida; falha em um único ramo da árvore |
| **Baixa** | Problema sem impacto na pessoa atendida | Erro de layout no painel; log com formatação incorreta |

Na dúvida entre duas classes, usar a mais grave.

## 2. Quem avisa e em quanto tempo

| Classe | Ação imediata | Comunicar | Prazo de comunicação |
|---|---|---|---|
| Crítica | Acionar parada de emergência (runbook, seção 4) | Responsável pela operação, responsável técnico, encarregado de dados | [a definir; sugestão: até 2 horas] |
| Alta | Avaliar se é necessário desligar o ramo afetado | Responsável técnico e responsável pela operação | [a definir; sugestão: até 24 horas] |
| Média | Corrigir na próxima janela de manutenção | Responsável técnico | Registro no `CHANGELOG.md` |
| Baixa | Corrigir quando possível | Nenhuma comunicação externa | Registro interno |

## 3. Vazamento ou acesso indevido a dados

Tratar como incidente crítico, independentemente de quão pequeno pareça.

1. Acionar a parada de emergência.
2. Preservar os registros de acesso e o estado do sistema, sem apagar nada.
3. Identificar quais dados foram afetados, quais pessoas são atingidas e desde quando.
4. Comunicar o encarregado de dados imediatamente, para avaliação de comunicação à Autoridade Nacional de Proteção de Dados (ANPD) e aos titulares, nos termos da LGPD.
5. Não comunicar pessoas atingidas sem orientação do encarregado de dados.
6. Registrar o incidente em `logs/incidentes.log`, com cronologia, dados afetados e medidas tomadas.

## 4. Erro de orientação sobre benefício

1. Identificar a regra afetada e a versão da árvore que a continha.
2. Desligar o ramo específico, se o erro puder se repetir.
3. Identificar pessoas que receberam a orientação incorreta. Se for possível contatá-las, fazê-lo pelo CRAS, com orientação revisada.
4. Corrigir a regra, com fonte oficial e data, e registrar no `CHANGELOG.md`.
5. Rodar a bateria de testes do ramo antes de reativar.
6. Registrar a causa raiz: erro na fonte, erro de interpretação ou erro de implementação.

## 5. Falha de caso de emergência

É sempre crítica, mesmo que a pessoa tenha recebido alguma orientação.

1. Acionar a parada de emergência imediatamente.
2. Verificar se a mensagem fixa com 192, 180 e 188 chegou à pessoa.
3. Reproduzir o caso com dados fictícios e adicionar o teste em `testes/emergencia/`.
4. Só reativar com a correção validada e aprovação por escrito, conforme o runbook.

## 6. Encerramento de incidente

Um incidente só é encerrado quando:
- a causa foi identificada e registrada;
- a correção foi aplicada e testada;
- o responsável técnico e o responsável pela operação foram informados;
- para incidentes críticos, o encarregado de dados confirmou a avaliação da comunicação à ANPD.

## 7. Revisão

Revisar este procedimento a cada incidente crítico ou alto, e no mínimo a cada seis meses.

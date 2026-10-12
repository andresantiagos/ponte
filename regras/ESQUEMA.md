# Esquema das regras de orientação

Cada regra da árvore de decisão é um bloco com os campos abaixo. Nenhuma regra entra em produção sem todos os campos preenchidos e a validação registrada.

## Campos obrigatórios

- **id:** identificador estável, no formato `ramo.nome` (exemplo: `salario_maternidade.periodo_graca`).
- **versao_arvore:** versão da árvore à qual a regra pertence (formato `AAAA.MM.NN`).
- **status:** `rascunho`, `validada` ou `revogada`. Só `validada` pode ir para produção.
- **pergunta:** texto exato da pergunta feita à pessoa.
- **opcoes:** lista de respostas fechadas. Respostas livres não entram na árvore.
- **desfecho:** para cada combinação de respostas, o desfecho, que é sempre um dos tipos abaixo.
- **fonte_oficial:** link ou referência da norma ou página oficial.
- **data_fonte:** data em que a fonte foi consultada.
- **validado_por:** nome e cargo de quem validou, ou `pendente`.
- **data_validacao:** data da validação, ou `pendente`.

## Tipos de desfecho

- `possibilidade_de_direito`: pode haver direito a X. Sempre com orientação para confirmar no CRAS ou no Meu INSS.
- `encaminhar_cras`: cadastro ou orientação social.
- `encaminhar_defensoria`: caso que pode exigir atuação jurídica. A escolha do advogado é sempre da pessoa.
- `emergencia`: mostrar 192, 180 e 188 e encerrar o fluxo de perguntas.
- `sem_possibilidade_aparente`: explicar o motivo e oferecer o CRAS. Nunca encerrar a conversa.

## Proibido em qualquer desfecho

- Declarar que a pessoa "é elegível" ou "não é elegível".
- Prometer valor, prazo ou concessão de benefício.
- Indicar escritório de advocacia ou pessoa específica.
- Mencionar cobrança.

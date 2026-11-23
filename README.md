# Comparação de extratores CNN para estimativa da largura de cordões PTA-DED

Código do TCC de Gustavo Sanches: comparação de InceptionResNetV2, ResNet50, DenseNet169 e EfficientNetB0 como extratores de características, com regressão estática e geração iterativa de atributos temporais.

## Notebooks

| Arquivo | Finalidade |
| --- | --- |
| [01 — Reprodução old](notebooks/01_old_adaptado.ipynb) | Reprodução das decisões da implementação de referência, incluindo suas limitações. |
| [02 — Desenvolvimento preliminar](notebooks/02_new_preliminar.ipynb) | Histórico de investigação e testes. Não é a entrada recomendada para uma campanha nova. |
| [03 — Pipeline consolidada](notebooks/03_new_consolidado.ipynb) | Entrada recomendada para executar os experimentos estáticos e temporais. |
| [04 — Comparativos](notebooks/04_comparativos.ipynb) | Carrega artefatos salvos e apresenta os gráficos, sem treinar modelos. |

Os quatro notebooks foram obtidos dos Colabs indicados pelo autor em 23/11/2026. As células de código e texto foram preservadas; saídas, contadores e metadados de execução foram removidos. O caminho de retomada da versão consolidada foi esvaziado para não apontar para uma execução particular.

## Execução recomendada

1. Abra `03_new_consolidado.ipynb` no Google Colab (Arquivo → Fazer upload do notebook, ou a aba GitHub após publicar este repositório).
2. Disponibilize no Drive os dados descritos em [docs/DADOS.md](docs/DADOS.md).
3. Execute a configuração e autorize a montagem do Drive.
4. Escolha `ARQUITETURA`, `USAR_PARAMETROS` e `USAR_DATASET_ANTIGO`. A base principal usa os perfis da Sofia; a base old é referência comparativa.
5. Para nova execução, use `RETOMAR_EXECUCAO = ''`. Confira caminhos e validações antes de habilitar o treinamento.
6. Ative `EXECUTAR_ESTATICO` e/ou `EXECUTAR_TEMPORAL` conforme a etapa pretendida. Ambos permanecem desativados por padrão.
7. Para os gráficos, abra `04_comparativos.ipynb`, configure `OUTPUT_ROOT` e `EXECUCOES` (nomes de pastas ou `TODAS`), conecte o Drive e carregue os resultados.

O notebook consolidado usa sementes 42 e 43 e avalia K = 0, 1, 5, 10, 25, 50 e 100 atributos temporais. A extração visual é reutilizada pela etapa temporal da mesma execução. Os regressores usam Dense(32, ReLU) → Dense(1).

## Protocolos e interpretação

A parte estática contém divisão aleatória, bloco central, bloco final e LOEO. A parte temporal consolidada contém bloco central e divisão aleatória. Os protocolos respondem a perguntas diferentes; seus conjuntos de avaliação não são intercambiáveis.

K=0 temporal é a referência estática pareada aos mesmos exemplos elegíveis para os demais K. Pode diferir do resultado estático que utiliza todos os exemplos de sua divisão.

Os atributos temporais são produzidos iterativamente por modelos auxiliares; não são simplesmente os valores medidos dos frames anteriores. Consulte o código consolidado e os registros das divisões para rastrear sua geração. Não confunda esse procedimento com as regras históricas de preenchimento e deslocamento do notebook old.

O notebook old reproduz decisões como ordenação original e reutilização da validação na avaliação, documentadas no próprio arquivo. Sua presença não significa que esses resultados constituam teste independente. Frames próximos podem ser correlacionados mesmo em um regressor que recebe imagens isoladas.

Os rótulos interpolados não são medições independentes por frame. A ordenação numérica não comprova a correspondência física imagem–largura. MAE menor em uma base de rótulos não comprova maior exatidão física dessa base.

## Ambiente e retomada

Os notebooks foram preparados para Google Colab e Google Drive. `requirements.txt` lista dependências diretas sem fixar versões não verificadas. Não se trata de um ambiente congelado; registre versões e hardware em cada campanha. Para execução fora do Colab, a montagem do Drive e os caminhos precisam ser adaptados.

Para retomar, informe em `RETOMAR_EXECUCAO` a pasta da execução consolidada e execute a configuração e as funções de preparação/validação antes da etapa pendente, conforme instruções no notebook. Preserve base, arquitetura, parâmetros e hiperparâmetros. Confira os checkpoints antes de repetir uma campanha.

Resultados ficam, por padrão, em `/content/drive/MyDrive/TCC/resultados/tcc_consolidado_v1/execucoes`. Dados, features e modelos não acompanham este repositório.

## Referências e proveniência

- Implementação de referência: [LeoFernanndes/temporal-cnn](https://github.com/LeoFernanndes/temporal-cnn).
- Reconstrução de perfis: [SophLafis/IC_ML_DED](https://github.com/SophLafis/IC_ML_DED).
- [Colabs de origem](docs/ORIGENS.md).

Este repositório preserva os notebooks de pesquisa, inclusive a versão preliminar, e não afirma equivalência exata entre as versões ou reprodução dos resultados sem os dados e o ambiente correspondentes.

## Licença

Uma licença de distribuição ainda não foi definida pelo autor. Antes de publicar, confira a atribuição e as condições aplicáveis ao código e aos dados de terceiros. Nenhuma licença de terceiros foi presumida ou substituída.

# Dados e artefatos

Os dados experimentais não estão incluídos.

Estrutura esperada pelo consolidado:

```text
/content/drive/MyDrive/TCC/
├── Dados Experimentos/
│   ├── experimentos_taguchi_400p_cropped_images.zip
│   └── cordon_width_profiles_dense_oriented.csv
└── resultados/
    └── tcc_consolidado_v1/
        └── execucoes/
```

O ZIP contém a pasta `experimentos_taguchi_400p_cropped_images`, subpastas L1 a L9 e imagens PNG numeradas. A pipeline extrai os arquivos para armazenamento temporário do Colab.

Os notebooks old e preliminar podem usar diretórios de saída diferentes. Confira a configuração de cada arquivo antes de executar. Para comparar execuções existentes, o painel precisa dos manifestos, índices, métricas, previsões e demais artefatos que cada visual lê. Copiar somente o CSV de resumo não substitui toda a execução.

Arquivos grandes (ZIP, NPY, NPZ, modelos Keras e resultados) são ignorados pelo Git. Disponibilização e autorização de uso dos dados devem ser tratadas com seus responsáveis.

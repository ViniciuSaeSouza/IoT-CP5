# 🚀 IoT-CP5: Redes Neurais e Visão Computacional

## 🎯 Objetivo do Projeto
Este projeto demonstra duas abordagens complementares de **Visão Computacional** aplicadas à **detecção e leitura de placas de motocicletas brasileiras**, além de um **exemplo de rede neural desenvolvida em Keras** (Parte 1 da CP5).

As soluções exploram:
1. 🧠 **Redes Neurais com Keras**  
2. 👁️ **Detecção e OCR com Hugging Face + Azure Vision**  
3. 🧩 **Workflow Roboflow** (fornecido em JSON para replicação)

---

## 🧠 Parte 01 – Redes Neurais (Keras)
### Exercício 1 – Classificação Multiclasse (Wine Dataset - UCI)

Neste exercício foi desenvolvida uma rede neural utilizando Keras para classificar vinhos em três classes, com base em 13 características físico-químicas do dataset Wine (UCI), **carregado pelo método load_wine do Scikit-learn.**
A rede neural foi configurada com:
* 2 camadas ocultas com 32 neurônios cada;
* Função de ativação ReLU nas camadas ocultas;
* Camada de saída com 3 neurônios e ativação Softmax;
* Função de perda categorical_crossentropy;
* Otimizador Adam.

Para comparação, também foram treinados os modelos RandomForestClassifier e LogisticRegression.
Os resultados mostraram que a **Rede Neural** e o **Random Forest** obtiveram **100% de acurácia**, enquanto a **Regressão Logística** atingiu **97,22%**.
No geral, ambos os primeiros tiveram o melhor desempenho, com o Random Forest sendo mais simples de treinar e interpretar.

---

### Exercício 2 – Regressão (California Housing Dataset)

Neste exercício, o objetivo foi treinar uma rede neural em Keras para realizar uma tarefa de **regressão**, prevendo o valor médio das casas no *California Housing Dataset*.
A rede neural foi configurada com:
* 3 camadas ocultas (64, 32 e 16 neurônios) com função de ativação ReLU;
* Camada de saída com 1 neurônio e ativação Linear (adequada para prever um valor contínuo);
* Função de perda Mean Squared Error (MSE);
* Otimizador Adam.

Para comparação, também foram utilizados os modelos Scikit-learn LinearRegression e RandomForestRegressor.
Os resultados foram avaliados pelas métricas de erro **RMSE** e **MAE** no conjunto de teste.

O **Random Forest Regressor** alcançou o melhor desempenho (RMSE: 0.5040, MAE: 0.3268). A **Rede Neural em Keras** demonstrou um desempenho robusto e competitivo (RMSE: 0.5292, MAE: 0.3602), superando significativamente a **Regressão Linear** (RMSE: 0.7456, MAE: 0.5332). O resultado da Keras valida a eficácia da arquitetura neural para a modelagem deste problema.

---

## 👁️ Parte 02 – Visão Computacional
Comparação entre duas ferramentas distintas aplicadas ao mesmo objetivo: **detectar e ler placas de veículos**.

### 🧰 Ferramentas Utilizadas
| Ferramenta | Uso Principal | Descrição |
|-------------|----------------|------------|
| 🤗 **Hugging Face (YOLOS)** | Detecção de placas | Modelo pré-treinado `nickmuchi/yolos-small-finetuned-license-plate-detection` |
| ☁️ **Microsoft Azure Computer Vision** | OCR (Image Analysis - READ API) | Extração de texto da placa detectada |
| 🧩 **Roboflow** | Workflow de visão e OCR | JSON disponível para replicação na plataforma Roboflow |

---

## 📁 Estrutura do Repositório
```
IoT-CP5/
├── notebooks/
│ └── CP5_AzureVC_2parte.ipynb # Detecção e OCR (Hugging Face + Azure)
├── workflows/
│ └── roboflow_workflow.json # Workflow exportável (para uso na plataforma Roboflow)
├── results/
│ ├── original_with_bbox.png
│ ├── cropped_plate.png
│ ├── ocr_plate.txt
│ └── metrics_hf_azure.json
├── images/
│ └── print_moto_placa.png # Imagem de teste
├── FINAL_Exemplo_Redes_Neurais_Com_Keras.ipynb
└── README.md
```
---

## 🧩 Dataset / Imagens
- 📸 Imagem de teste: `images/print_moto_placa.png`  
- 📚 Dataset público (Roboflow):  
  👉 [Roboflow Universe Dataset's](https://universe.roboflow.com/zeroexperiments/motorcycle-license-plate-skrdr)

---

## ⚙️ Hiperparâmetros e Configurações Principais (Visão Computacional)
| Parâmetro | Valor | Descrição |
|------------|--------|-----------|
| Modelo | `nickmuchi/yolos-small-finetuned-license-plate-detection` | Detecção de placas |
| Threshold de confiança | `0.5` | Filtro mínimo de detecção |
| Pré-processamento | Conversão RGB + crop dinâmico | Otimiza a entrada do OCR |
| OCR | Azure AI Vision Image Analysis (READ) | Extração de caracteres da placa |

---

## ▶️ Como Executar

### 🔧 Configuração de Ambiente
Defina suas variáveis de ambiente no sistema ou `.env`:
```bash
VISION_ENDPOINT=<seu_endpoint_azure>
VISION_KEY=<sua_chave_azure>
GEMINI_API_KEY=<sua_chave_gemini>
```
### 💻 Execução

1. Execute o notebook principal:
 ```bash
  notebooks/CP5_AzureVC_2parte.ipynb
```
2. Os resultados e métricas serão gerados na pasta `results/`.

---

🌐 Testar o Workflow do Roboflow

Para testar a abordagem alternativa:

1. Acesse Roboflow

2. Crie um novo Workflow.

3. Copie o conteúdo do arquivo: `workflows/roboflow_workflow.json`
  e cole na interface da plataforma.

⚖️ Comparativo entre as Abordagens
| Critério              | 🤗 Hugging Face + Azure                 | 🧩 Roboflow                            |
| --------------------- | --------------------------------------- | -------------------------------------- |
| **Configuração**      | Executado localmente via notebook       | Interface visual, executado em nuvem   |
| **Flexibilidade**     | Alta – livre escolha de modelo e OCR    | Média – depende do pipeline criado     |
| **OCR**               | Azure Vision (alta precisão)            | OCR integrado (precisão variável)      |
| **Latência média**    | ~2 segundos / imagem                    | ~4–5 segundos / imagem                 |
| **Custo**             | OCR pago por requisição                 | Gratuito até certo limite              |
| **Reprodutibilidade** | Notebook Python (totalmente replicável) | Workflow JSON (copiável na plataforma) |

---

## 📊 Resultados e Observações

📂 Resultados salvos em results/:

original_with_bbox.png → imagem com bounding box

cropped_plate.png → recorte da placa

ocr_plate.txt → texto lido via OCR

metrics_hf_azure.json → métricas de latência e confiança

## 🧩 Conclusões

O modelo YOLOS apresentou alta precisão em placas no padrão Mercosul.

O OCR do Azure demonstrou robustez mesmo sob variação de iluminação.

O Roboflow se mostrou útil para validação rápida e replicação do pipeline.

---

## 🎥 Vídeo de Demonstração

👉 Assista à demonstração no [YouTube](https://youtu.be/cPnyaplA49Ahttps://youtu.be/cPnyaplA49A)

---

### 🏆 Integrantes

| Nome                              | RM     | GitHub                                             |
| --------------------------------- | ------ | -------------------------------------------------- |
| **Laura de Oliveira Cintra**      | 558843 | [@Laura-Cintra](https://github.com/Laura-Cintra)   |
| **Maria Eduarda Alves da Paixão** | 558832 | [@MariaEdPaixao](https://github.com/MariaEdPaixao) |
| **Vinícius Saes de Souza**        | 554456 | [@ViniciuSaeSouza](https://github.com/ViniciuSaeSouza) |

✨ Projeto desenvolvido como parte da disciplina Disruptive Architectures: IoT, IoB & Generative AI – FIAP 2025.


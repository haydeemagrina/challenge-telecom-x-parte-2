Readme
O notebook Telecom_II_novo.ipynb é um projeto de ciência de dados aplicado à análise de churn (cancelamento de clientes) em uma empresa de telecomunicações. O projeto inclui tratamento de dados, modelagem preditiva e avaliação de modelos com foco em interpretação e desempenho.
O objetivo principal deste projeto é identificar clientes propensos ao cancelamento e compreender os principais fatores que influenciam essa decisão, com foco em aplicações práticas para retenção de clientes.

Ele inclui as seguintes etapas:
1.	Tecnologias e Bibliotecas Utilizadas
- Python 3.x
- Pandas – Manipulação de dados
- Plotly Express – Visualização interativa de dados
- Scikit-learn – Modelagem e avaliação (train_test_split, DummyClassifier,   DecisionTreeClassifier, etc.)
2.	Importação do arquivo dados_tratados_tudo.csv, arquivo que foi tratado no Chalenge Telecom X – 1ª parte.
3.	Definição de variáveis explicativas (X) e variável alvo (churn = y).
4.	Análise gráfica utilizando histogramas do Churn x variáveis explicativas (gender, Senior Citizen, Partner, Dependents, PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, Device Protection, TechSupport, StreamingTV, StreamingMovies, Contract, PaperlessBilling e Faixa de Custo Diário. Objetivo de avaliar quais variáveis tem forte influência sobre o churn.
5.	Importação da plotly.express
6.	Análise gráfica do churn x variáveis numéricas (tenure, Charges.Monthly e Charges.Total)
7.	Preparação dos dados:
o	Verificação de todas as colunas tem a mesma quantidade de linhas
o	Transformação das variáveis categóricas em valores numéricos inteiros 
8.	Divisão dos dados:
o	Separação dos dados em treino e teste com train_test_split .
9.	Modelagem Preditiva:
o	Modelos utilizados:
	Dummy Classifier (modelo base). – Acurácia= 0.712, AUC-ROC: 0.5000
	Árvore de Decisão. – Acurácia= 0.708, AUC-ROC: 0.6271
	KNN – Acurácia = 0.753, AUC-ROC: 0.7163
	XGBoost – Acurária = 0.756, AUC-ROC: 0.7794
o	
10.	Visualizações:
o	Uso de bibliotecas como matplotlib.pyplot  para visualizar a árvore de decisão graficamente. Acurácia treino = 0,981
o	Definir profundidade máxima da árvore para 3 decisões.
	 Acurácia treino = 0,772
	Acurácia teste = 0,768
o	Normalização com o KNN -  Acurácia teste = 0,753

11.	Avaliação dos Modelos:
o	Acurácia Dummy: 0.7121629058888277 = 71,22%
o	Acurácia Árvore de Decisão: 0.7682993946064942 = 76,83%
o	Acurácia KNN: 0.7534397358282884 = 75,34%
o	Acurácia XGBoost – Acurária = 75,65%

12.	Ajuste fino (tuning) no XGBoost: Melhor AUC-ROC RandomizedSearch: 0.8234865398980579
Interpretação:
Parâmetro	Significado	Impacto observado
subsample=0.6	Usa 60% dos dados em cada árvore → aumenta robustez	Reduz overfitting, melhora generalização
n_estimators=200	200 árvores → mais aprendizado	Mais tempo, mas melhora performance
max_depth=4	Árvores rasas → menos complexidade	Reduz overfitting, equilíbrio ideal
learning_rate=0.01	Passos pequenos no aprendizado	Modelo aprende lentamente, mais preciso
colsample_bytree=0.8	Usa 80% das features por árvore	Reduz correlação entre árvores, melhora diversidade
________________________________________
Comparação com XGBoost padrão:
•	AUC padrão XGBoost: 0.7565 (do seu teste anterior)
•	AUC com ajuste fino: 0.8235 → significativa melhora
________________________________________
Conclusão:
O modelo ajustado está mais robusto e generaliza melhor.
A AUC-ROC acima de 0.82 indica que o modelo tem boa capacidade de separação entre churn e não churn.

13.	Avaliação real com melhores parâmetros RandomizedSearch
Análise da Curva ROC: Elemento Descrição TPR (True Positive Rate) Mostra a taxa de acertos positivos reais do modelo. Quanto mais perto de 1, melhor. FPR (False Positive Rate) Mostra a taxa de falsos positivos. Quanto mais perto de 0, melhor. Curva azul Representa o desempenho do modelo. Linha preta tracejada Linha de referência (classificação aleatória, AUC = 0.5). AUC = 0.81 Bom desempenho. Modelos com AUC entre 0.8 e 0.9 são considerados bons.
Interpretação: O modelo XGBoost ajustado tem boa capacidade discriminativa para classificar corretamente entre as classes (ex: churn vs não churn).
O fato da curva estar bem acima da linha aleatória indica que o modelo aprendeu padrões úteis nos dados.

14.	Conclusão:
Variáveis mais influentes:
1.	Contract_Month-to-month (onehotencoder__Contract_Month-to-month)
o	Está na raiz da árvore ⇒ maior impacto na separação entre churn e não churn.
o	Clientes com contrato mensal tendem a ter maior propensão ao churn.
2.	tenure
o	Segunda variável usada ⇒ indica o tempo que o cliente está com a empresa.
o	Clientes com menor tenure (menos tempo de casa) têm mais churn.
3.	InternetService_Fiber optic
o	Clientes com fibra ótica tendem a apresentar maior churn comparado aos que usam DSL ou nenhum serviço.
4.	Contract_Two year
o	Contrato de 2 anos aparece mais abaixo, mas ainda relevante.
o	Clientes com contratos longos (2 anos) têm menor churn.

Conclusão:
A variável mais influente é Contract_Month-to-month, seguida por tenure. Isso indica que clientes com contrato mensal e pouco tempo de casa são mais propensos ao churn.
Conclusão:
•	XGBoost já tinha a melhor curva ROC e maior AUC (0.78), indicando que é o modelo mais confiável para prever churn. O ajuste fino (tunning) no XGBoost aumentou AUC = 0.82 e sugere que, ao comparar aleatoriamente um cliente churn e um não churn, o modelo tem 82% de chance de rankear o churn corretamente acima do não churn.
•	KNN também é razoável, mas pode ser menos prático dependendo do volume de dados.
•	Árvore de Decisão é significativamente inferior em termos de AUC, apesar da boa acurácia. É boa alternativa se quiser explicabilidade e rapidez.
•	O Dummy mostra que qualquer modelo mais inteligente que ele vale a pena usar.

Recomendação:
Use XGBoost — ele é robusto, mais preciso e seu desempenho é consistente mesmo com classes desbalanceadas, como é comum em problemas de churn.

Insights Estratégicos:
1.	Foco em retenção inicial: Intervir cedo pode ser eficaz — churn está associado a pouco tempo de uso.
2.	Programas de fidelização: Incentivar permanência com benefícios progressivos pode aumentar Charges.Total e reduzir churn.
3.	Foco na retenção inicial: Intervenções nos primeiros meses são críticas. Pode valer a pena oferecer:
•	Descontos nos primeiros meses.
•	Benefícios por fidelidade progressiva.
•	Contato proativo com suporte.

Implicações práticas:
•	Atenção especial aos clientes novos nos primeiros 1 a 12 meses, pois estão mais propensos ao churn.
•	Estratégias de retenção podem ser mais eficazes se focadas nos clientes com tenure abaixo da mediana (~15 meses).
•	Monitorar o comportamento e satisfação nos primeiros meses de serviço é essencial para reduzir o churn.
•	Segmentação por cobrança: Clientes com cobranças acima da mediana geral (~70) devem ser monitorados com mais atenção.
•	Estratégia de retenção: Pode ser interessante oferecer descontos ou planos personalizados para clientes com cobranças mensais mais altas.
•	Modelagem preditiva: Charges.Monthly é uma feature importante e pode melhorar a capacidade preditiva de um modelo de churn.


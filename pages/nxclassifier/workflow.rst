***********************************************
Entendendo o fluxo de trabalho do NxClassifier
***********************************************

É preciso entender o fluxo de trabalho do NxClassifier antes você pode criar uma regra de classificação eficaz para você.

NxClassifier por si só é um programa multi-tarefa dentro do NxFilter. Quando o NxFilter recebe a requisição de um domínio não requisitado, ele adiciona o domínio em uma fila de processos do NxClassifier. NxClassifier faz verifica o DNS para ver se o domínio já está registrado e então tenta acessar o site desse domínio. Se há um website o NxClassifier baixa essa página e analisa o título, descrição e o texto.

Uma vez que o NxClassifier obtém os detalhes de um website então ele executa as regras de classificação com base nos dados coletados. Enquanto está executando a verificação dos dados, se ele encontrar uma regra que se encaixe com o dados, ele para e classifica o dominio de acordo a categoria definida na regra. Ainda soma a pontuação a outras regras já identificadas e classifica do dominio em uma categoria cuja pontuação máxima seja atingida.

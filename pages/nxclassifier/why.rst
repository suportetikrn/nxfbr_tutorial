*****************************
Pot que usar o NxClassifier?
*****************************

Há duas formas que podem ser usadas como método de Classificação para montar uma lista.

1. Auto-Classificação

2. Classificação manual

A auto-classificação é uma tarefa executada de forma extremamente rápida, porém não é tão assertiva quanto a classificação manual. E a classificação manual tem um custo elevado tanto em trabalho quanto financeiro pois precisa de pessoas dedicadas a essa funcionalidade.

Então a melhor forma é combinar os dois métodos ou diminuir o máximo a necessidade da avaliação humana se baseando nos resultados da auto-classificação.

Diversas ferramentas de classificação automática fazem essa função baseadas em ocorrências de palavras chave usando dicionários ou algum tipo de conjunto de regras. Então precisamos fazer um dicionário de palavras mais eficaz ou conjunto de regras para uma auto-classificação com resultados satisfatõrios. Porém é possível haver opiniões diferentes com relação a que categoria se aplica a uma determinada ocorrência e o nível de importância dessa ocorrência comparada a outras.

Por exemplo, ``www.stackoverflow.com`` é classificado como uma  `Comunidade` ou um `Fórum` mas também pode ser classificado como na categoria `Computer/Technology` já que o foco do site é exatamente computador e tecnologias. E ainda pode estar na categoria `Business/Service`. Nós podemos classificá-lo em multiplas categorias. Porém no caso analisado podemos encontrar outro problema. E se quisermos bloquear `Forum` mas permitir o acesso `Computer/Technology`? Podemos acabar obtendo um resultado inesperado.

Outro ponto a se observar, a lista de classificação padrão é feita em Inglês mas essa não é a única linguagem no mundo. Existem muitos sites em outras línguas. Então é preciso ter dicionários em outras línguas também. Porém como contruir todos esses dicionários visando atender as outras línguas? E se fizermos classificação manual ou a verificação é preciso atender públicos que falam outras língas. Então as necessidades tomam uma dimensão maior e ninguém tem interesse de arcar com isso. Com isso passamos a ter falsos positivos e desse modo passa a ser impossível ter uma lista que atenda 100% dos casos.

É bom observar que uma lista não pode atender a toda a internet. Mesmo que se tenha arquivos extensos que vizem cobrir toda a Internet, quantos sites registrados nessa lista podem realmente ser úteis para seu caso? A maioria dos sites listados nunca seriam acessados por seus usuários.

Contudo com NxClassifier você tem:

1. Você cria suas próprias regras.

   Significa que você pode criar suas regras de classificação de acordo com sua necessidade. Nada melhor que você para classificar os sites em sua própria língua.

2. Não são permitidas múltiplas categorias 

   Um site só pode ser classificado em uma única categoria.

.. note::

   O motivo para que provedores de listas tenham categorias múltiplas para um único site não é apenas refletir a ambiguidade existente no mundo real. Eles utilizam isso forma a fim de atender mercados/clientes diversos, por isso precisam ter sites classificados em múltiplas categorias mas isso não atende a nossa necessidade em muitos casos.
 
3. Você pode re-categorizar um site instântaneamente.
   
  Não precisa esperar que um provedor aceite e atenda sua solicitação de mudança de categoria para um ou vários sites. Você pode alterar sua lista de acordo com sua necessidade.

4. Jahaslist em crescimento contínuo

  Visando deixar o pacote do NxFilter pequeno, o sistema vem com uma lista mínima embutida. Ela atende os principais sites. Mas visando assessorar a classificação dinâmica do NxClassifier e de acordo com o uso ela vai sendo alimentada e mantém os sites usados pelos seus usuários.

5. Você pode compartilhar suas listas e regras com outros.

  Uma vez que você tenha criado sua própria lista usando NxClassifier você pode compartilhá-la com outros. E não somente a lista, você pode compartilhar também suas regras de classificação.


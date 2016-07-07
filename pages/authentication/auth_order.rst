A Ordem dos métodos/modos de autenticação
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxFilter permite diversas formas de autenticação ao mesmo tempo. Porém há uma ordem a ser seguida. Você precisa entender essa ordem para poder montar sua configuração de controle.


A ordem é:

1. Associar a um determinado IP

Essa associação é a primeira, então verifica se o endereço IP está associado a uma determinado faixa ou permitir alguns usuários se autenticar sem o procedimento de login.


2. Sessão por IP

Sessão por IP é o login sendo criado e mantido no NxFilter através de SSO ou página de login, exatamente nessa ordem. 
 
3. IP range association 

Quando se faz necessário permitir o acesso de um usuário qualquer sem que este precise se autenticar você pode criar/associar o mesmo a uma faixa de IPs que cubra toda a sua rede. 

Mas você pode desejar distinguir os usuários fazendo a associação através de um único IP ou Sessão por IP. Então o vínculo ao range de IPs é aplicado por último.

Então temos a ideia de que 'Se aplica primeiro o range mais próximo'. Se houver faixas de IP cadastradas, quanto menor a faixa maior a prioridade de aplicação antes das outras faixas.


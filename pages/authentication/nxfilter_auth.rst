********************************
NxFilter e Autenticação
********************************

Porquê autenticar?
^^^^^^^^^^^^^^^^^^

Quando o NxFilter é instalado ele vem com somente uma política e ela é aplicada a todos os usuários da sua rede. Porém como faria se você estivesse trabalhando para uma escola - por exemplo - como administrador de sistemas e você deseja aplicar uma política baseada em usuários e grupos? Criando para estudantes uma política mais rígida e para professores uma política menos restritiva sem ter como identificá-los? Então é preciso distinguir os usuários ativando a autenticação.

Que autenticação usar?
^^^^^^^^^^^^^^^^^^^^^^^

Nxfilter tem suporte a diversos modos de autenticação. É possível escolher um deles ou mesclá-los de modo a identificar através de um deles.

1. Autenticação baseada em IP
  O modo mais simples de autenticação. Quando se usa IP estático no desktop está pode ser a melhor alternativa. Apenas um endereço IP associado a um usuário criado na GUI do NxFilter. É possivel também associar uma faixa de IPs a um usuário.

.. note::
  Muitas pessoas tentam usar a autenticação baseada em IP sem ativar a mesma em 'Config > Setup'. Porém a autenticação baseada em endereço IP ainda precisa que seja habilitado antes o método de autenticação.

2. Autenticação baseada em Senha
  
  Quando é ativada a autenticação o NxFilter bloqueia qualquer usuário que tentar usar a Internet, apresentando a página de Login - a menos que já tenham se autenticado ou tenham seu endereço IP já associado. Para passar da página de login seus usuários precisam entrar com as senhas definidas antes. Você pode setar a senha para cada usuário na GUI NxFilter.

3. Autenticação baseada em LDAP

  Se você tem um servidor OpenLDAP ou AD, seus usuários pode se autenticar usando as mesmas credenciais registradas no LDAP. 

.. alert::
  Para usar essa funcionalidade você precisa importar seus usuários do servidor LDAP antes.

4. Login token based authentication

NxFilter has a special concept called 'Login Token'. This is used for remote user authentication or filtering. This login token is being created for each user when you create or import users. You use this login token to differentiate users for remote user filtering with NxClient and NxBlock or dynamic IP update with NxUpdate.
5. Single sign-on against Active Directory
Many people want to filter their users transparently. Or you don't want to show any login prompt to your users. NxFilter provides Active Directory integration. Once you implement it your users don't need to go through NxFilter's login-page and your users will be appeared on NxFilter GUI with their Active Directory usernames and groups.


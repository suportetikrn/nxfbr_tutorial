A Ordem dos métodos/modos de autenticação
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxFilter permite diversas formas de autenticação ao mesmo tempo. Porém há uma ordem a ser seguida. Você precisa entender essa ordem para poder montar sua configuração de controle.


A ordem é:

1. Associar a um determinado IP

Essa associação é a primeira, então verifica se o endereço IP está associado a uma determinado faixa ou permitir alguns usuários se autenticar sem o procedimento de login.


2. Sessão por IP

Sessão por IP é o login sendo criado e mantido no NxFilter através de SSO ou página de login, exatamente nessa ordem. 
 
3. IP range association 

When you need to allow an anonymous user to access the Internet without any login process you create an IP range user to cover whole your network. But you still want to differentiate users by single IP association or the login session. So the IP range association comes at last.

We have 'Most specific IP range comes first' rule for ordering IP range users. If there are overlapped IP ranges the smaller IP range will be applied before the others.


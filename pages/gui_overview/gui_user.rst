GUI - User
^^^^^^^^^^^
You can create or import users and groups here. NxFilter supports user importation from Active Directory and OpenLDAP.

Criando o usuário
*****************

Para criar um usuário vá em 'User & Group > User'. Existem 3 tipos de usuários no NxFilter

1. IP user 
 O Usuário tem um endereço de IP ou um Range de IPs e será autenticado vinculado a ele(s).

2. Password user 
 Se você definir uma senha para um usuário ele se classifica como 'password user'. Você pode usar a senha para se autenticar no NxFilter.

3. LDAP user 
 Quando você importa usuários dos servidores LDAP ou AD ele se tornam `LDAP users`. Podem usar as credenciais definidas no servidor LDAP ou AD na página de login do NxFilter.

Propriedades do usuário
************************
- Password : A senha usada para se autenticar
- Work-time Policy : A política que será aplicada quando não estiver em horário livre.
- Free-time Policy : A política aplicada durante o horário livre. Você pode definir o horário livre em 'Policty- & Rule > Free Time'.
- Expiration Date : Data em que a conta de usuário expira
- Login Token : Token para filtro em usuários remotos ou autenticação dos mesmos. É criado automaticamente quando o usuário é criado ou importado.

Testando um usuário
*******************
Quando você tem usuários importados através do LDAP este pode estar cadastrado em diversos grupos e políticas. Como resultado disso fica a dificuldade em determinar que política será aplicada ao mesmo. Para saber que política vem sendo aplicada ao usuário use o botão 'Test' na listagem dos usuários e verifique o campo 'Applied Policy', isso informa os dados do usuário naquele momento.

.. note::

   Você pode usar a visão de teste para verificar também a quota ou o volume de dados utilizado por um determinado usuário ou até resetar esses limites.

Criando um grupo
*****************

Pode-se criar um grupo em 'User & Group > Group'. Após a criação de um grupo é possível definir uma política para este grupo através da edição de suas propriedade. Nessa mesma área pode também atribuir mebros ao grupo.


Importando usuários e grupos a partir do LDAP ou AD

Você pode importar usuários e grupos do AD em 'User & GRoup > Active Directory'. 

Por exemplo, se você tem nas instalações um AD nos seguintes moldes ::

 - Controlador de Domínio: 192.168.0.100
 - Domínio : nxfilter.local
 - Login de Administrador : Administrator

Você definirá os parâmetros dessa forma:
- Host : 192.168.0.100
- Admin : Administrator@nxfilter.local
- Password : your-password
- Base DN : cn=users,dc=nxfilter,dc=local
- Domain : nxfilter.local

Após ter feito a configuração do AD você pode importar os usuários e grupo clicando em 'IMPORT'. Pode ainda definir que essa definir que a importação seja executada periódicamente selecionando um intervalor de tempo na opção 'auto-sync'.

.. note::
  Para verificar o funcionamento clique no botão 'TEST'


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
- Login Token : The token for remote user filtering or remote user authentication. It is created when a user created or imported.
Testing a user
When you have an LDAP imported user you may have multiple groups and policies for a user. As a result it becomes difficult to figure out which policy a user fall into. To find out which is the 'Applied Policy' for a user, use 'TEST' button on the user list. It fetches the state of a user from NxFilter in real-time way.
* You can use this test view to find out how much quota or bandwidth consumed by a user or to reset quota or bandwidth for a user.
Creating a group
You can create a group on 'User & Group > Group'. After you create a group you can set up a policy for the group by editing its properties. You also can assign members to the group.
Importing users and groups from Active Directory or OpenLDAP
You can import users and groups from Active Directory on 'User & Group > Active Directory'. For example, if you have your Active Directory with the following setup.
- Domain controller : 192.168.0.100
- Domain : nxfilter.local
- Admin username : Administrator
Then you can create an Active Directory importation setup with the following details.
- Host : 192.168.0.100
- Admin : Administrator@nxfilter.local
- Password : your-password
- Base DN : cn=users,dc=nxfilter,dc=local
- Domain : nxfilter.local
After having an Active Directory importation setup you can import users and groups with 'IMPORT' button. You also can set up a periodical import by selecting an auto-sync interval.
* If you want to find out if there is a connectivity issue between NxFilter and your domain controller, use 'TEST' button.


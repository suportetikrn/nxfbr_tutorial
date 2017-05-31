Como usar o JahasFilter
^^^^^^^^^^^^^^^^^^^^^^^

Já que o JahasFilter por dentro continua sendo o NxFilter, você pode usá-lo do mesmo modo que o NxFilter. Porém para o caso de pessoas que nunca tiveram experiência com o serviço de filtro, vamos dar alguns exemplos de como usá-lo.


Como bloquear o Facebook usando JahasFilter
-------------------------------------------

Após ter configurado os seus PCs para usar somente o JahasFilter como servidor DNS, vá em 'User & Policy > Policy' na GUI de administração e altere a política 'Default' e marque para bloquear a categoria 'Social Networking'.

.. note::
   
   Pode levar algum tempo para que a sua política seja aplicada nos clientes já que eles tem seu próprio Cache DNS.
   

.. image:: /images/jahasfilter-policy.png

Autenticando com o JahasFilter
------------------------------

Diferente do NxFilter, JahasFilter só da suporte a autenticação baseada em IP. E há uma diferença na forma em como o NxFilter faz a autenticação baseada em IP.

Unlike NxFilter, JahasFilter supports IP based authentication only. And there's one thing different from NxFilter's way of IP based authentication. Since we have seen so many people tried to associate a user to an IP address without enabling authentication we made the IP association working without authentication enabled on JahasFilter. This means you can identify or view your users with their username and apply a policy when you create a user on JahasFilter GUI and associate the user to an IP or IP range.
However, it is user identification. It's not authentication yet. Users not having associated IP or unknown users will be able to use your network still. If you want to block these unknown users, go to 'Config > Setup' and enable 'Block Unknown User'. Then only the users having username and associated IP will be able to use your network.
* We have a preference of IP based authentication. Single IP association comes first and then smaller IP range. You can make some exception to your filtering policy using this rule. For example, you can associate '192.168.0.1 ~ 192.168.0.255' to a user named 'everyone' and associate '192.168.0.100' to 'manager' and assign a different policy on him/her.


Se você tem um AD
---------------------

Para facilitar, o JahasFilter não dá suporte a integração com AD. Mas não siginifica que você não possa usar o JahasFilter em seu ambiente com AD. Você ainda pode fazer com que o JahasFilter trabalhe em conjunto com o servidor DNS MS. Só precisa fazer com que o seja feito a liberação do domínio AD no servidor DNS MS. Por exemplo, se seu domínio for 'nxfilter.local' e considerando que seu servidor AD esteja na rede '192.168.0.x'  e o IP do seu servidor é '192.168.0.254'. Em 'DNS > Setup > Local DNS', defina :

 - Local DNS Server : 192.168.0.254
 - Local Domain : nxfilter.local, 0.168.192.in-addr.arpa

Desse modo o controle da rede ocorrerá sem quebrar o acesso a seu AD.


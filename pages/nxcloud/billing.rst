Criando Bilhetagem própria
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

É possíver ter no serviço do NxCloud, falando comercialmente, um sistema de bilhetagem automática. Tendo por base que todas as páginas da GUI são disponibilizadas para alteração, não haverá dificuldade para criar seus próprio sistema de bilhetagem com o NxCloud.

Para implementar seu próprio sistema de bilhetagem pode - por exemplo - ser necessário criar, editar um operador que esteja vinculado a conta do seu cliente no seu serviço de DNS. Você dever estar apto a executar esse procedimento em suas próprias páginas JSP. 

Supondo que haja a necessidade de criar um operador com os atributos abaixo:

- Name : triton
- Password : triton1234
- Email : tmail0487@yahoo.com
- Max user : 3
- Max user IP : 3
- Max policy : 3
- Max whitelist : 20
- Max free-time : 10

A página JSP deverá estar com os seguintes comandos:

.. code-block:: jproperties
  <%
	OperatorData data = new OperatorData();
	data.name = ”triton”;
	data.passwd = ”triton1234”;
	data.email = ”tmail0487@yahoo.com”;
	data.max_user = 3;
	data.max_user_ip = 3;
	data.max_policy = 3;
	data.max_whitelist = 20;
	data.max_free_time = 10;
	OperatorDao dao = new OperatorDao();
	dao.insert(data);
   %> 


Se precisa atualizar alguns dados do operador :


.. highlight:: java
    <%
	OperatorDao dao = new OperatorDao();
	OperatorData data = dao.select_one_by_name(”triton”);
	data.max_user = 5;
	data.max_user_ip = 5;
	data.max_policy = 5;
	dao.update(data);
    %>

Se você precisa desativar um operador :

 .. highlight:: java
    <%
     	OperatorDao dao = new OperatorDao();
	OperatorData data = dao.select_one_by_name(”triton”);
	data.stop_flag = true;
	dao.update(data);
    %>


.. note::
     
   Há uma seção, nesta documentação, dedicada exclusivamente a customização da GUI e também é disponibilizado o Javadoc para facilitar a criação da suas própria GUI.

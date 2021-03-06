GUI - Acessando a base de dados
*********************************

Geralmente na programação web, o uso de um banco de dados é algo muito importante. 

No NxFilter/NxOEM são utilizados 'Data Access Object' e 'Data Object' para manipular o Banco de Dados.


Métodos utilizados para manipular os 'Data Access Object'
----------------------------------------------------------

Alguns métodos são usados para acessar a maioria dos dados. 

Por exemplo. em 'policy,policy.jsp'  são usadas as classes PolicyDao e PolicyData class para manipular as Políticas. PolicyDao tem os seguinte métodos:

.. code-block:: java

   public int select_count() : Quantidade de políticas.
   public List select_list() : Retornar uma lista contendo as políticas
   public PolicyData select_one(int id) : Retornar uma determinada política com base no ID.
   public boolean insert(PolicyData data) : Insere uma nova política
   public boolean update(PolicyData data) : Atualiza uma política existente.
   public boolean delete(int id) : Apaga/Remove uma política com determinado ID.

Cada política tem seu próprio ID que é um número e pode ser usado para encontrar e atualizar uma determinada política.


Inserir, remover, atualizar, selecionar registros
----------------------------------------------------

Se há o interesse em modificar ''whitelist,domain.jsp'' tem de se usar as classes 'WhitelistDomainDao' e 'WhitelistData'.

Inserir um novo registro,

.. code-block:: jsp

 <%
   WhitelistDomainDao dao = new WhitelistDomainDao();
   WhitelistData data = new WhitelistData();
   data.domain = "*.nxfilter.org";
   data.bypass_auth = true;
   data.bypass_filter = true;
   dao.insert(data);
  %>

Para remover um registro cujo ID é igual a 12,

.. code-block:: jsp

   <%
    WhitelistDomainDao dao = new WhitelistDomainDao();
    dao.delete(12);
   %>

Para selecionar um registro com ID igual a 12,

.. code-block:: jsp

   <%
    WhitelistDomainDao dao = new WhitelistDomainDao();
    WhitelistData data = dao.select_one(12);
   %>

E para atualizar o registro selecionado,

.. code-block:: jsp

   <%
     data.bypass_filter = false;
     dao.update(data);
   %>

E listar os registros.

.. code-block:: jsp

   <%
    WhitelistDomainDao dao = new WhitelistDomainDao();
    List data_list = dao.select_list();
    for(WhitelistData data : data_list){
       out.println(data.domain + "<br>");
    }
   %>

Accessing data field
---------------------

Muitos desenvolvedores Java estão usando accessors 'get' e 'set' visando encapsular e para fazer outros procedimentos como validar os registros. Para para facilitar, na maioria do casos é permitido o acesso direto ao campo.

Por exemplo, se criar uma instância de UserData e ele tiver a propriedade ''name'', deverá ser feito como o exemplo:

.. code-block:: jsp
   <%
	UserData data = new UserDao().select_one(1);
	out.println(data.name)
   %>

Porém, existem muitas classes que tem os métodos começando por 'get_'. Geralmente esses métodos são vinculados a formatação. Há a propriedade ''ctime'' para 'RequestData' que é usado em ''Logging > Request''. Se usar a chamada direta, obterá como retorno '201507081415', já se chamar o método 'get_ctime()' será retornado ''07/08 14:14''.

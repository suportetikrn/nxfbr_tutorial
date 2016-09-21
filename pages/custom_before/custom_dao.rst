GUI - Acessando a base de dados
*********************************

Geralmente na programação web, o uso de um banco de dados é muito importante. No NxFilter/NxOEM São utilizados 'Data Access Object' e 'Data Object' para manipular o Banco de Dados.


Métodos utilizados para manipular os 'Data Access Object'
----------------------------------------------------------

Alguns métodos são usados para acessar a maioria dos dados. Por exemplo. em 'policy,policy.jsp'  são usadas as classes PolicyDao e PolicyData class para manipular as Políticas. 

PolicyDao tem os seguinte métodos:

.. code-block:: java

public int select_count() : The number of policies.
public List select_list() : Fetching policies as a list.
public PolicyData select_one(int id) : Fetching one policy by ID column.
public boolean insert(PolicyData data) : Insert a new policy.
public boolean update(PolicyData data) : Update a existing policy.
public boolean delete(int id) : Delete a policy by ID column.
Every policy data has its own unique ID which is a number and we use this ID for finding, updating a policy data.
Insert, delete, update, select data
If we want to modify 'whitelist,domain.jsp' we have to use 'WhitelistDomainDao' and 'WhitelistData' classes.
To insert a new data,

.. code-block:: jsp

 <%
   WhitelistDomainDao dao = new WhitelistDomainDao();
   WhitelistData data = new WhitelistData();
   data.domain = "*.nxfilter.org";
   data.bypass_auth = true;
   data.bypass_filter = true;
   dao.insert(data);
  %>

To delete a data when its ID is 12,
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
Many Java developers are using 'get' and 'set' accessors for encapsulation and for having some additional data processing like validation. But for simplicity, we use a public field directly in most cases. For example, you get an instance of UserData and uses its 'name' property like the following codes,
<%
UserData data = new UserDao().select_one(1);
out.println(data.name)
%>
However there are some data classes having methods starting with 'get_'. These methods are mostly about formatting. We have 'ctime' property for 'RequestData' which we use on 'Logging > Request'. If you use it directly you get '201507081415' but when you use its 'get_ctime()' method you get '07/08 14:14'.

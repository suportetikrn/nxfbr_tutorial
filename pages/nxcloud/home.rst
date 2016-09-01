*********************************
Tipos de Contas Business and Home
*********************************

Quando você criar um serviço de filtragem baseado nas nuvens um dos problemas que você tem é como definir o número de usuários na rede interna. É mais fácil quando você tem um tipo de agente instalado e sendo executado dentro dessa rede e NxCloud suporta diversos agentes para esse caso.

Em todo caso alguns de seus clientes não podem
When you build a cloud based filtering service one of the problems you have is to find out the exact number of users behind a router. It may be possible when there are some kind of agent installed and running behind router and NxCloud supports several agents for that. However some of your customers don't need to differentiate users and they just want to have one global policy for everybody. It means you don't know how many users they have.
To solve this problem, we limit the request count for a user. Currently one user can make 3,000 requests a day. This is more than enough considering a user makes under 1,000 requests a day according to our statistics so far. However we may have another issue from this request count limit approach. If you have a customer using your service in their home they probably have several Internet accessing devices and have several family members but not wanting to pay for multiple users. In that case this 3,000 daily request limit is too small for them.
To address this issue, we introduced the concept of operator type. There are 2 kinds of operator types on NxCloud. One is 'Business' and the other is 'Home'. Business type operators are nothing special. You can create as many users as you want for them and each of the users has 3,000 request limit. But if it is a home type operator its first user has 12,000 extra request count and that makes 15,000 daily request count limit for the first user. If it has the second user its request count limit becomes 18,000 and that would be more than enough for most home users.

.. note::
  
  Pàra um operador residencial você pode criar acima de 5 usuários

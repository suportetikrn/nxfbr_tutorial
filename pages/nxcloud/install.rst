*********************
Instalação do NxCloud
*********************

 NxCloud é - basicamente - um NxFilter modificado. Você pode instalar e rodar o NxCloud da mesma forma que o NxFilter.

 Porém, diferente do NxFilter, após instalá-lo você ainda não pode usá-lo diretamente como um servidor DNS. Isto é por que o foco de NxCloud é para venda de serviços comerciais. Você - teoricamente - não o usará na sua rede interna ( por conta de custos de licença e etc ). Seus clientes o utilizarão em suas redes. Então é necessário primeiro criar uma conta para seu cliente.
 
 No NxCloud há 3 tipos de usuários:
 1. Admin - que é você ou a empresa responsável pela instalação do NxCloud.
 2. Operador - que é seu cliente
 3. Usuário - Que é o usuário da rede do seu cliente.

 O `admin` gerencia as contas dos operadores e um `operador` gerencia o `usuário` final.
 
 Então é preciso que você crie antes o `operador`. Para isso acesse a GUI do NxCloud ( como `admin` ) e então vá ao menu `Operator` para criar o `operador`.

 Ao criar um operador haverá - por padrão - um usuário e uma política para o operador com o mesmo nome deste. E a senha padrão para o operador é o nome do mesmo. Uma vez criado um operador é possível que este se autentique na GUI a fim de criar um usuário de teste.

.. note::
   Você precisa associar seu endereço IP para que o operador inicial possa testar o o usuário padrão.


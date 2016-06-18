Instalando o NxCloud
^^^^^^^^^^^^^^^^^^^^^^

NxCloud nada mais é que um NxFilter modificado. É possível instalar e executar o NxCloud da mesma forma como é feito com o NxFilter.

Porém diferente do NxFilter, após sua instalação, você ainda não pode usar o servidor DNS. Isso por que o NxCloud é um programa para atender múltiplos clientes visando prestar um serviço comercial. É suposto que você não o usará na sua rede interna. Seus clientes é que o usarão em suas redes. Então você precisa criar uma conta para cada um dos seus clientes primeiro.

No NxCloud existem 3 tipos de usuários:
 
  Admin > Operator > User

  1. Admin - é você, que administra todos os operadores.
  
  2. Operator - É o seu cliente, ele gerencia os usuários finais e as políticas. 

  3. User - É o usuário final, o usuário do serviço DNS.

  Então é necessário criar antes o operador. Para fazer isso entre na GUI do NxCloud como administrador e então vá ao menu 'Operator'. Você pode criar um operador nessa área.

  Quando for criado um operador ele terá criado por padrão um usuário e uma política como o mesmo nome do operador. E a senha padrão para o operador é também o seu nome. Uma vez que seja criado um operador é possível se autenticar com a conta do mesmo e configurar um usuário para testes.

  ::
  É preciso associar seu endereço IP ao usuário padrão do seu primeiro operador para poder testá-lo.


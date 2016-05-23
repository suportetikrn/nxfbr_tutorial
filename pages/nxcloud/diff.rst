*************************************
Diferenças entre NxFilter e NxCloud 
*************************************

1. Autenticação sempre habilitada

   Nem todo o serviço disponibilizado por você deverá ser gratuito. Você querendo disponibilizar o serviço apenas para assinantes então a autenticação é habilitada por padrão.
 
2. Redirecionamento de Login desabilitado por padrão

   É possivel usar a página de login com NxCloud mas se você usar o mesmo em uma rede pública pode acabar sendo alvo de um ataque DDOS.
    
   Seria melhor desabilitar o acesso vindo de alguma rede pública. Quando NxCloud é desabilitado ele simplesmente destrói os pacotes de requisição DNS vindos de redes desconhecidas.

3. 'Magic Password' para acesso do operador a GUI

   Como um administrador de NxCloud algumas vezes você precisará acessar a GUI para um possível suporte técnico. Por essa razão, NxCloud tem uma senha a mais para a administração.
   É chamada de 'Magic password'. Com a qual é possível acessar o ambiente de administração. A 'magic password' é `magic1023` e você pode alterar a senha em `Config > Admin`.


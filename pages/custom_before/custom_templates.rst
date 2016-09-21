Modelos para email e página de bloqueio
****************************************

NxFilter envia emails de alera para o administrador. 

Geralmente esses emails são sobre tentativas de acesso a sites bloqueados porém há também emails sobre falhas no cluster ou violação de licença. Há dois modelos de email para esses alertas.

    - /nxfilter/conf/tpl/access_violation.ftl

    - /nxfilter/conf/tpl/alert_email.ftl

No diretório '/nxfilter/conf/tpl' é possível encontrar os modelos de páginas de bloqueio, login e boas-vindas. Esses modelos são utilizados na instalação inicial do NXFilter para popular o Banco de Dados ou quando você clica em 'RESTORE-DEFAULT' em ''Config > Block Page'' na GUI NxFilter.


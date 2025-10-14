---
title: Adicionar e configurar usuários
description: As configurações de Gerenciamento de usuários no console de administração permitem criar ou excluir usuários e definir outras configurações de usuário.
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 0%

---

# Adicionar e configurar usuários {#adding-and-configuring-users}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

As informações de usuários e grupos são mantidas em um sistema de armazenamento de terceiros, como um diretório LDAP. O gerenciamento de usuários não grava no sistema de armazenamento de terceiros. Em vez disso, o Gerenciamento de usuários sincroniza as informações do usuário e do grupo com seu próprio banco de dados

## Criar um usuário {#create-a-user}

Ao criar usuários, você pode adicioná-los a grupos e atribuir funções a eles.

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]** e em **[!UICONTROL Novo usuário]**.
.
1. Em **[!UICONTROL Configurações Gerais]**, forneça as informações necessárias e clique em **[!UICONTROL Avançar]**. Para obter detalhes sobre as configurações, consulte [Configurações do usuário](adding-configuring-users.md#user-settings).
1. (Opcional) Para adicionar o usuário a um grupo, clique em **[!UICONTROL Localizar Grupos]** e execute estas tarefas:

   * Na caixa **[!UICONTROL Localizar]**, digite todo o nome do grupo ou parte dele.
   * Selecione o domínio a ser pesquisado, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.
   * (Opcional) Para exibir detalhes do grupo, selecione o nome do grupo e clique em **[!UICONTROL OK]** para retornar à página de resultados da pesquisa.
   * Marque a caixa de seleção do grupo e clique em **[!UICONTROL OK]**.
   * Clique em **[!UICONTROL Avançar]**.

1. (Opcional) Para atribuir funções ao usuário, clique em **[!UICONTROL Localizar Funções]**, marque a caixa de seleção das funções a serem atribuídas e clique em **[!UICONTROL OK]**.
1. Clique em **[!UICONTROL Concluir]**.

   >[!NOTE]
   >
   >Se você encontrar algum problema de logon com o usuário, consulte [Falha do usuário do AEM Forms no JEE ao fazer logon no AEM Forms no OSGi &#x200B;](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Configurações do usuário {#user-settings}

Especifique as configurações a seguir ao criar ou editar um usuário.

**Nome Canônico:** (Obrigatório) Identificador exclusivo do usuário. Cada usuário e grupo em um domínio deve ter um nome canônico exclusivo. Marque a caixa de seleção Gerado pelo Sistema para permitir que o Gerenciamento de Usuários atribua um valor exclusivo ou desmarque a caixa de seleção e especifique um valor personalizado para o Nome Canônico.

Evite usar caracteres de sublinhado (_) em nomes canônicos, por exemplo, `sample_user`. Quando você pesquisa usuários com base em seus nomes canônicos, os que contêm caracteres sublinhados não são retornados.

**Nome:** (Obrigatório) Nome fornecido pelo usuário

**Sobrenome:** (Obrigatório) Nome da família do usuário

**Nome Comum:** Nome completo ou nome para exibição do usuário. Por exemplo, se Nome = Gloria e Sobrenome = Rios, então Nome comum = Gloria Rios.

**Email:** endereço de email do usuário

**Telefone:** número de telefone do usuário

**Descrição:** Descrição opcional. Use esse campo conforme as necessidades da sua organização.

**Endereço:** endereço para correspondência do usuário

**Organização:** organização à qual o usuário pertence

**Aliases de email:** Aliases de email do usuário. Separe os aliases de email com vírgulas.

**Domínio:** Domínio ao qual o usuário pertence

**Localidade:** localidade ISO do usuário

**Chave do Calendário Comercial:** permite mapear um calendário comercial para um usuário, com base no valor dessa configuração. Os calendários comerciais definem dias úteis e não úteis. Os formulários AEM podem usar calendários comerciais ao calcular datas e horas futuras para eventos, como lembretes, prazos finais e escalonamentos. A forma como você atribui chaves do calendário de negócios aos usuários depende de você estar usando um domínio corporativo, local ou híbrido. (Consulte [Adicionar domínios](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Se você estiver usando um domínio local ou híbrido, as informações sobre os usuários serão armazenadas somente no banco de dados do Gerenciamento de usuários. Para esses usuários, defina a Chave do calendário comercial como uma string. Em seguida, mapeie a chave do calendário comercial (a sequência de caracteres) para um calendário comercial no fluxo de trabalho de formulários.

Se você estiver usando um domínio enterprise, as informações sobre usuários residirão em um sistema de armazenamento de terceiros, como um diretório LDAP. O Gerenciamento de usuários sincroniza as informações do usuário do diretório com o banco de dados do Gerenciamento de usuários. Esse recurso permite mapear uma chave de calendário comercial para um campo no diretório LDAP. Por exemplo, considere um cenário em que cada registro de usuário no diretório contém um campo de país e você deseja atribuir calendários de negócios com base no país em que o usuário está localizado. Nesse caso, você especifica o nome do campo do país como o valor para a configuração Chave do calendário comercial. Em seguida, é possível mapear as chaves do calendário comercial (os valores definidos para o campo de país no diretório LDAP) para calendários comerciais no fluxo de trabalho de formulários.

Para obter informações adicionais sobre calendários comerciais, incluindo como mapear chaves de calendários comerciais para calendários comerciais, consulte [Configurando Calendários Comerciais](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limite o nome a menos de 53 caracteres. Um nome mais curto ajuda a evitar problemas na exibição da chave do calendário de negócios nas páginas de Gerenciamento de processos no console de administração.

**ID de Usuário:** (Obrigatório) ID de Usuário que o usuário usa para fazer logon. A ID de usuário não diferencia maiúsculas de minúsculas e deve ser exclusiva no domínio.

Em domínios enterprise, use um atributo não DN como a ID do usuário, pois o DN de um usuário poderá ser alterado se ele for movido para outra parte da organização. Esta configuração depende do servidor de diretório. O valor é `objectGUID` para o Ative Diretory 2003, `nsuniqueID` para o Sun™ One e `guid` para o eDirectory.

Certifique-se de que a ID do usuário seja exclusiva. Não use um atribuído a um usuário excluído.

Os formulários AEM não conseguem diferenciar entre contas de usuário que têm IDs de usuário e senhas idênticas, mas pertencem a domínios diferentes. Para evitar esse problema, não crie contas que tenham a mesma ID de usuário em vários domínios.

Ao usar o SQL Server como banco de dados, você não pode criar uma ID de usuário que exceda 255 caracteres.

Ao usar o MySQL, a ID do usuário pode conter caracteres estendidos. No entanto, quando uma comparação é feita entre duas cordas, como abcde e âbcdè, elas são consideradas a mesma. Por exemplo, durante a sincronização, se um novo usuário foi adicionado ao banco de dados, uma comparação é feita para verificar se um usuário com a mesma ID de usuário existe no banco de dados. Se o usuário *abcde* existir no banco de dados quando o novo usuário *âbcdè* for adicionado, a comparação não poderá distinguir entre os dois nomes. Pressupõe-se que o usuário exista no banco de dados e o novo usuário seja ignorado e não adicionado.

Evite criar nomes de usuário que comecem com um sinal numérico (#). A execução de pesquisas de tarefas não retorna nenhum resultado para esses nomes de usuário. (Consulte [Trabalhar com tarefas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Senha e Confirmar Senha:** Senha que o usuário usa para fazer logon. Deve ter no mínimo oito caracteres. Uma senha não é necessária para um usuário que faz parte de um domínio híbrido.

## Exibir detalhes sobre um usuário {#view-details-about-a-user}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Especifique informações para restringir a pesquisa e, na lista Em, selecione Usuários e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. Você pode classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do usuário sobre o qual exibir detalhes. A página Editar Usuário exibe os detalhes abaixo sobre o usuário:

   * Informações gerais de identificação, como nome, email, endereço, domínio e organização
   * Funções atribuídas ao usuário
   * Grupos dos quais o usuário é membro

## Alterar a senha de um usuário local {#change-the-password-for-a-local-user}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Especifique informações para restringir a pesquisa para um usuário específico e clique em **[!UICONTROL Localizar]**. Os resultados da pesquisa são listados na parte inferior da página. Você pode classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do usuário e em **[!UICONTROL Alterar Senha]**.
1. Digite e confirme a nova senha e clique em **[!UICONTROL OK]**. A senha deve ter no mínimo oito caracteres.

## Editar as propriedades de um usuário {#edit-a-user-s-properties}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Para localizar o usuário a ser editado, execute estas tarefas:

   * Na caixa **[!UICONTROL Localizar]**, digite seus critérios de pesquisa.
   * Na lista **[!UICONTROL Usando]**, selecione **[!UICONTROL Nome]**, **[!UICONTROL Email]** ou **[!UICONTROL ID de Usuário]**.
   * Na **[!UICONTROL Lista de entrada]**, selecione **[!UICONTROL Usuários]**.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.

1. Clique no usuário para editar.
1. Para um usuário que faça parte de um domínio local ou híbrido, na guia **[!UICONTROL Detalhes]**, edite as **[!UICONTROL Configurações Gerais]** e as **[!UICONTROL Configurações de Logon]** e clique em **[!UICONTROL Salvar]**. Para obter detalhes sobre as configurações, consulte [Configurações do usuário](adding-configuring-users.md#user-settings). Não é possível editar as configurações gerais e de login de um usuário que pertença a um domínio enterprise.
1. Para editar as configurações de grupo do usuário, clique na guia **[!UICONTROL Associação de Grupo]** e execute estas tarefas:

   * Clique em **[!UICONTROL Localizar Grupo]** e preencha as informações de pesquisa.
   * Para adicionar o usuário a um novo grupo, marque a caixa de seleção do grupo, clique em **[!UICONTROL OK]** e em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >Usuários locais não podem ser adicionados a grupos de diretórios. No entanto, os usuários do diretório podem ser adicionados a grupos locais.

   * Para remover o usuário de um grupo, marque a caixa de seleção do grupo, clique em **[!UICONTROL Excluir]** e em **[!UICONTROL Salvar]**.

1. Para editar as funções do usuário, clique na guia **[!UICONTROL Atribuições de função]** e execute estas tarefas:

   * Para exibir uma lista de funções, clique em **[!UICONTROL Localizar Funções]**.
   * Para adicionar uma função, marque a caixa de seleção da função, clique em **[!UICONTROL OK]** e em **[!UICONTROL Salvar]**.
   * Para remover uma função, marque a caixa de seleção da função, clique em **[!UICONTROL Cancelar atribuição]** e em **[!UICONTROL Salvar]**.

## Excluir um usuário {#delete-a-user}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Para localizar o usuário a ser excluído, execute estas tarefas:

   * Na caixa **[!UICONTROL Localizar]**, digite seus critérios de pesquisa.
   * Na lista **[!UICONTROL Usando]**, selecione **[!UICONTROL Nome]**, **[!UICONTROL Email]** ou **[!UICONTROL ID de Usuário]**.
   * Na **[!UICONTROL Lista de entrada]**, selecione **[!UICONTROL Usuários]**.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.

1. Marque a caixa de seleção do usuário, clique em **[!UICONTROL Excluir]** e em **[!UICONTROL OK]**.

>[!NOTE]
>
>O AEM Forms no JEE também permite que os usuários do complemento AEM forms em execução em um OSGi sejam reconhecidos como usuários do AEM. Isso é necessário para cenários em que o logon único entre o AEM Forms no JEE e o complemento AEM de formulários em execução em um OSGi é necessário (por exemplo, espaço de trabalho do HTML). A operação de exclusão mencionada acima remove um usuário somente do AEM Forms no JEE. O usuário não é excluído do complemento AEM Forms em execução no ambiente OSGi. Mas qualquer tentativa de logon feita após a exclusão do usuário (uma tentativa de logon no servidor JEE do complemento AEM Forms ou no ambiente OSGi do complemento AEM Forms) é negada.

## Criar manipulador de erro de logon personalizado {#create-custom-login-error-handler}

Se um usuário sem os formulários AEM e as permissões do CQ necessários tentar fazer logon nos seguintes aplicativos incorporados ao CQ, o usuário será redirecionado para a página padrão do CQ 404 que contém o rastreamento de erros:

* Solução de gerenciamento de correspondência
* AEM Forms Workspace

  ***observação &#x200B;**: o Flex Workspace foi descontinuado para a versão de formulários AEM.*

* gerenciador de formulários
* Relatório de processo

O CQ fornece um mecanismo para substituir o jsp do manipulador 404 padrão.

Para obter detalhes sobre como personalizar a página de tratamento de erros, consulte [Personalizando páginas mostradas pelo Manipulador de erros](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=pt-BR) na documentação do Adobe Experience Manager.

---
title: Adicionar e configurar usuários
seo-title: Adding and configuring users
description: As configurações de Gerenciamento de usuários no console de administração permitem criar ou excluir usuários e definir outras configurações de usuário.
seo-description: The User Management settings in the administration console allow you to create or delete users  and configure other user settings.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# Adicionar e configurar usuários {#adding-and-configuring-users}

As informações do usuário e do grupo são mantidas em um sistema de armazenamento de terceiros, como um diretório LDAP. O Gerenciamento de usuários não grava no sistema de armazenamento de terceiros. Em vez disso, o Gerenciamento de usuários sincroniza as informações do usuário e do grupo com seu próprio banco de dados

## Criar um usuário {#create-a-user}

Ao criar usuários, você pode adicioná-los a grupos e atribuir funções a eles.

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]** e clique em **[!UICONTROL Novo usuário]**. .
1. Em **[!UICONTROL Configurações gerais]**, forneça as informações necessárias e clique em **[!UICONTROL Próximo]**. Para obter detalhes sobre as configurações, consulte [Configurações do usuário](adding-configuring-users.md#user-settings).
1. (Opcional) Para adicionar o usuário a um grupo, clique em **[!UICONTROL Localizar Grupos]** e execute estas tarefas:

   * No **[!UICONTROL Localizar]** , digite parte ou todo o nome do grupo.
   * Selecione o domínio a pesquisar, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.
   * (Opcional) Para exibir detalhes do grupo, selecione o nome do grupo e clique em **[!UICONTROL OK]** para retornar à página de resultados da pesquisa.
   * Marque a caixa de seleção do grupo e clique em **[!UICONTROL OK]**.
   * Clique em **[!UICONTROL Avançar]**.

1. (Opcional) Para atribuir funções ao usuário, clique em **[!UICONTROL Localizar Funções]**, marque a caixa de seleção das funções a serem atribuídas e clique em **[!UICONTROL OK]**.
1. Clique em **[!UICONTROL Concluir]**.

   >[!NOTE]
   >
   >Se encontrar algum problema de logon com o usuário, consulte [O AEM Forms no usuário JEE falha ao fazer logon no AEM Forms no lado OSGi](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Configurações de usuário {#user-settings}

Especifique as seguintes configurações ao criar ou editar um usuário.

**Nome Canônico:** (Obrigatório) Identificador exclusivo para o usuário. Cada usuário e grupo em um domínio deve ter um nome canônico exclusivo. Marque a caixa de seleção Sistema gerado para permitir que o Gerenciamento de usuários atribua um valor exclusivo, ou desmarque a caixa de seleção e especifique um valor personalizado para o Nome canônico.

Evite usar caracteres sublinhados (_) em nomes canônicos, por exemplo, `sample_user`. Quando você pesquisa usuários com base em seu nome canônico, aqueles que contêm caracteres sublinhados não são retornados.

**Nome:** (Obrigatório) Nome do usuário

**Sobrenome:** (Obrigatório) Nome da família do usuário

**Nome comum:** Nome completo ou nome de exibição para o usuário. Por exemplo, se First Name = Gloria e Last Name = Rios, então Common Name = Gloria Rios.

**Email:** Endereço de email do usuário

**Telefone:** Número de telefone do usuário

**Descrição:** Descrição opcional. Use esse campo conforme as necessidades da sua organização.

**Endereço:** Endereço de correspondência do usuário

**Organização:** Organização à qual o usuário pertence

**Aliases de email:** Aliases de email do usuário. Separe os aliases de email com vírgulas.

**Domínio:** Domínio ao qual o usuário pertence

**Localidade:** Local ISO do usuário

**Chave do Calendário Comercial:** Permite mapear um calendário comercial para um usuário, com base no valor dessa configuração. Os calendários de negócios definem dias úteis e não úteis. AEM formulários podem usar calendários de negócios ao calcular datas e horários futuros para eventos como lembretes, prazos e escalonamentos. A forma como você atribui chaves do calendário de negócios aos usuários depende se você está usando um domínio corporativo, local ou híbrido. (Consulte [Adição de domínios](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Se você estiver usando um domínio local ou híbrido, as informações sobre os usuários serão armazenadas somente no banco de dados do Gerenciamento de usuários . Para esses usuários, defina a Chave do Calendário Comercial como uma sequência de caracteres. Em seguida, mapeie a chave do calendário comercial (a string) para um calendário comercial no fluxo de trabalho de formulários.

Se você estiver usando um domínio corporativo, as informações sobre os usuários ficarão em um sistema de armazenamento de terceiros, como um diretório LDAP. O Gerenciamento de usuários sincroniza as informações do usuário do diretório com o banco de dados do Gerenciamento de usuários. Esse recurso permite mapear uma chave do calendário de negócios para um campo no diretório LDAP. Por exemplo, considere um cenário em que cada registro de usuário em seu diretório contém um campo de país e deseja atribuir calendários de negócios com base no país em que o usuário está localizado. Nesse caso, você especifica o nome do campo do país como o valor para a configuração Chave do calendário comercial . Em seguida, você pode mapear as chaves do calendário de negócios (os valores definidos para o campo do país no diretório LDAP) para calendários de negócios no fluxo de trabalho de formulários.

Para obter informações adicionais sobre calendários de negócios, incluindo como mapear chaves de calendário de negócios para calendários de negócios, consulte [Configurando Calendários Comerciais](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limite o nome para menos de 53 caracteres. Um nome mais curto ajuda a evitar problemas ao exibir a chave do calendário de negócios nas páginas de Gerenciamento de Processos no console de administração.

**ID de usuário:** (Obrigatório) ID de usuário que o usuário usa para fazer logon. A ID de usuário não diferencia maiúsculas e minúsculas e deve ser exclusiva no domínio.

Em domínios corporativos, use um atributo que não seja DN como ID de usuário, pois o DN de um usuário pode ser alterado caso se mova para outra parte da organização. Essa configuração depende do servidor de diretório. O valor é `objectGUID` para o Ative Diretory 2003, `nsuniqueID` Sun™ One e `guid` para eDirectory.

Certifique-se de que a ID do usuário seja exclusiva. Não use um que tenha sido atribuído a um usuário excluído.

AEM formulários não podem diferenciar entre contas de usuário com IDs de usuário e senhas idênticas, mas pertencem a domínios diferentes. Para evitar esse problema, não crie contas que tenham a mesma ID de usuário em vários domínios.

Ao usar o SQL Server como banco de dados, não é possível criar uma ID de usuário que exceda 255 caracteres.

Ao usar o MySQL, a ID do usuário pode conter caracteres estendidos. No entanto, quando uma comparação é feita entre duas strings, como abcde e âbcdè, elas são consideradas iguais. Por exemplo, ao sincronizar, se um novo usuário foi adicionado ao banco de dados, é feita uma comparação para verificar se um usuário com a mesma ID de usuário existe no banco de dados. Se usuário *abcde* existe no banco de dados quando o novo usuário *âbcdè* for adicionada, a comparação não poderá distinguir entre os dois nomes. Pressupõe-se que o usuário exista no banco de dados e que o novo usuário seja ignorado e não adicionado.

Evite criar nomes de usuário que comecem com um sinal de número (#). Realizar pesquisas de tarefa não retorna resultados para esses nomes de usuário. (Consulte [Trabalhar com tarefas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Senha e confirmação de senha:** Senha que o usuário usa para fazer logon. Deve ter no mínimo oito caracteres. Uma senha não é necessária para um usuário que faz parte de um domínio híbrido.

## Exibir detalhes sobre um usuário {#view-details-about-a-user}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Especifique informações para restringir a pesquisa e, na lista Em, selecione Usuários e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. Você pode classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do usuário para exibir detalhes sobre o. A página Editar usuário exibe detalhes como abaixo sobre o usuário:

   * Informações gerais de identificação, como nome, email, endereço, domínio e organização
   * Funções atribuídas ao usuário
   * Agrupa que o usuário é membro de

## Alterar a senha de um usuário local {#change-the-password-for-a-local-user}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Especifique as informações para limitar a pesquisa de um usuário específico e clique em **[!UICONTROL Localizar]**. Os resultados da pesquisa são listados na parte inferior da página. Você pode classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do usuário e, em seguida, clique em **[!UICONTROL Alterar senha]**.
1. Digite e confirme a nova senha e clique em **[!UICONTROL OK]**. A senha deve ter no mínimo oito caracteres.

## Editar as propriedades de um usuário {#edit-a-user-s-properties}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Para localizar o usuário a ser editado, faça o seguinte:

   * No **[!UICONTROL Localizar]** digite seus critérios de pesquisa.
   * No **[!UICONTROL Usando]** lista, selecione **[!UICONTROL Nome]**, **[!UICONTROL Email]** ou **[!UICONTROL ID de usuário]**.
   * No **[!UICONTROL Na lista]**, selecione **[!UICONTROL Usuários]**.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.

1. Clique no usuário para editar.
1. Para um usuário que faz parte de um domínio local ou híbrido, no **[!UICONTROL Detalhe]** edite a guia **[!UICONTROL Configurações gerais]** e **[!UICONTROL Configurações de logon]** e clique em **[!UICONTROL Salvar]**. Para obter detalhes sobre as configurações, consulte [Configurações do usuário](adding-configuring-users.md#user-settings). Não é possível editar as configurações gerais e de logon de um usuário que pertence a um domínio empresarial.
1. Para editar as configurações de grupo do usuário, clique no botão **[!UICONTROL Associação de Grupo]** e execute estas tarefas:

   * Clique em **[!UICONTROL Localizar Grupo]** e preencha as informações de pesquisa.
   * Para adicionar o usuário a um novo grupo, marque a caixa de seleção do grupo e clique em **[!UICONTROL OK]** e, em seguida, clique em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >Usuários locais não podem ser adicionados a grupos de diretórios. No entanto, os usuários do diretório podem ser adicionados a grupos locais.

   * Para remover o usuário de um grupo, marque a caixa de seleção do grupo e clique em **[!UICONTROL Excluir]** e, em seguida, clique em **[!UICONTROL Salvar]**.


1. Para editar as funções do usuário, clique no botão **[!UICONTROL Atribuições de Função]** e execute estas tarefas:

   * Para exibir uma lista de funções, clique em **[!UICONTROL Localizar Funções]**.
   * Para adicionar uma função, marque a caixa de seleção da função, clique em **[!UICONTROL OK]** e, em seguida, clique em **[!UICONTROL Salvar]**.
   * Para remover uma função, marque a caixa de seleção da função, clique em **[!UICONTROL Cancelar atribuição]** e, em seguida, clique em **[!UICONTROL Salvar]**.

## Excluir um usuário {#delete-a-user}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Para localizar o usuário a ser excluído, faça o seguinte:

   * No **[!UICONTROL Localizar]** digite seus critérios de pesquisa.
   * No **[!UICONTROL Usando]** lista, selecione **[!UICONTROL Nome]**, **[!UICONTROL Email]** ou **[!UICONTROL ID de usuário]**.
   * No **[!UICONTROL Na lista]**, selecione **[!UICONTROL Usuários]**.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.

1. Marque a caixa de seleção do usuário e clique em **[!UICONTROL Excluir]** e, em seguida, clique em **[!UICONTROL OK]**.

>[!NOTE]
>
>O AEM Forms no JEE também permite que os usuários do complemento AEM forms em execução em um OSGi sejam reconhecidos como usuários AEM. Isso é necessário para cenários em que o logon único entre o AEM Forms no JEE e AEM complemento de formulários em execução em um OSGi é necessário (por exemplo, HTML workspace). A operação de exclusão acima mencionada remove um usuário somente do AEM Forms no JEE. O usuário não é excluído do complemento AEM Forms em execução no ambiente OSGi. Mas qualquer tentativa de logon feita após excluir o usuário (uma tentativa de logon no servidor JEE do complemento AEM Forms ou no complemento AEM Forms no ambiente OSGi) é negada.

## Criar manipulador de erros de logon personalizado {#create-custom-login-error-handler}

Se um usuário sem os formulários de AEM necessários e as permissões do CQ, tentar fazer logon nos seguintes aplicativos incorporados ao CQ, o usuário será redirecionado para a página padrão do CQ 404 que contém o rastreamento de erro:

* Solução de gerenciamento de correspondência
* Espaço de trabalho de formulários AEM

   ***observação **: O Flex Workspace está obsoleto para a versão AEM formulários.*

* gerenciador de formulários
* Relatório de processo

O CQ fornece um mecanismo para substituir o manipulador padrão 404 jsp.

Para obter detalhes sobre como personalizar a página de tratamento de erros, consulte [Personalização de páginas mostradas pelo Manipulador de erros](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) na documentação do Adobe Experience Manager.

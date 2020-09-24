---
title: 'Adicionar e configurar usuários '
seo-title: 'Adicionar e configurar usuários '
description: As configurações de Gerenciamento de usuários no console de administração permitem que você crie ou exclua usuários e defina outras configurações de usuário.
seo-description: As configurações de Gerenciamento de usuários no console de administração permitem que você crie ou exclua usuários e defina outras configurações de usuário.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---


# Adicionar e configurar usuários {#adding-and-configuring-users}

As informações de usuários e grupos são mantidas em um sistema de armazenamentos de terceiros, como um diretório LDAP. O Gerenciamento de usuários não grava no sistema de armazenamentos de terceiros. Em vez disso, o Gerenciamento de usuários sincroniza as informações do usuário e do grupo com seu próprio banco de dados

## Criar um usuário {#create-a-user}

Ao criar usuários, você pode adicioná-los a grupos e atribuir funções a eles.

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]** e clique em **[!UICONTROL Novo usuário]**.
.
1. Em Configurações **** gerais, forneça as informações necessárias e clique em **[!UICONTROL Avançar]**. Para obter detalhes sobre as configurações, consulte Configurações [](adding-configuring-users.md#user-settings)do usuário.
1. (Opcional) Para adicionar o usuário a um grupo, clique em **[!UICONTROL Localizar grupos]** e faça as seguintes tarefas:

   * Na caixa **[!UICONTROL Localizar]** , digite parte ou todo o nome do grupo.
   * Selecione o domínio a ser pesquisado, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.
   * (Opcional) Para visualização dos detalhes do grupo, selecione o nome do grupo e clique em **[!UICONTROL OK]** para retornar à página de resultados da pesquisa.
   * Marque a caixa de seleção do grupo e clique em **[!UICONTROL OK]**.
   * Clique em **[!UICONTROL Avançar]**.

1. (Opcional) Para atribuir funções ao usuário, clique em **[!UICONTROL Localizar funções]**, marque a caixa de seleção das funções a serem atribuídas e clique em **[!UICONTROL OK]**.
1. Click **[!UICONTROL Finish]**.

   >[!NOTE]
   >
   >Se você encontrar algum problema de login com o usuário, consulte Falha do usuário do [AEM Forms no JEE ao fazer login no AEM Forms no lado](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html)do OSGi.

## Configurações de usuário {#user-settings}

Especifique as seguintes configurações ao criar ou editar um usuário.

**Nome Canônico:** (Obrigatório) Identificador exclusivo para o usuário. Cada usuário e grupo em um domínio deve ter um nome canônico exclusivo. Marque a caixa de seleção Gerado pelo sistema para permitir que o Gerenciamento de usuários atribua um valor exclusivo ou desmarque a caixa de seleção e especifique um valor personalizado para o Nome canônico.

Evite usar caracteres sublinhados (_) em nomes canônicos, por exemplo, `sample_user`. Quando você pesquisa usuários com base em seu nome canônico, aqueles que contêm caracteres sublinhados não são retornados.

**Nome:** (Obrigatório) Nome próprio do usuário

**Sobrenome:** (Obrigatório) Nome da família do usuário

**Nome comum:** Nome completo ou nome de exibição para o usuário. Por exemplo, se Nome = Gloria e Sobrenome = Rios, então Nome comum = Gloria Rios.

**Email:** Endereço de email do usuário

**Telefone:** Número de telefone do usuário

**Descrição:** Descrição opcional. Use esse campo conforme as necessidades de sua organização.

**Endereço:** Endereço de correspondência do usuário

**Organização:** Organização à qual o usuário pertence

**Aliases de email:** Aliases de email do usuário. Separe os alias de e-mail por vírgulas.

**Domínio:** Domínio ao qual o usuário pertence

**Local:** Local ISO do usuário

**Chave do Calendário Comercial:** Permite mapear um calendário de negócios para um usuário, com base no valor dessa configuração. Os calendários de negócios definem dias úteis e não úteis. AEM formulários podem usar calendários de negócios ao calcular datas e horários futuros para eventos como lembretes, prazos e escalonamentos. A forma como você atribui chaves de calendário de negócios aos usuários depende se você está usando um domínio corporativo, local ou híbrido. (Consulte [Adicionar domínios](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Se você estiver usando um domínio local ou híbrido, as informações sobre os usuários serão armazenadas somente no banco de dados Gerenciamento de usuários. Para esses usuários, defina a Chave do calendário comercial como uma string. Em seguida, mapeie a chave do calendário comercial (a sequência) para um calendário comercial no fluxo de trabalho dos formulários.

Se você estiver usando um domínio corporativo, as informações sobre os usuários ficarão em um sistema de armazenamentos de terceiros, como um diretório LDAP. O Gerenciamento de usuários sincroniza as informações do usuário do diretório com o banco de dados Gerenciamento de usuários. Esse recurso permite mapear uma chave do calendário comercial para um campo no diretório LDAP. Por exemplo, considere um cenário em que cada registro de usuário em seu diretório contenha um campo de país e você deseja atribuir calendários de negócios com base no país em que o usuário está localizado. Nesse caso, especifique o nome do campo do país como valor para a configuração Chave do calendário comercial. Em seguida, é possível mapear as chaves do calendário comercial (os valores definidos para o campo do país no diretório LDAP) para os calendários de negócios no fluxo de trabalho dos formulários.

Para obter informações adicionais sobre calendários de negócios, incluindo como mapear chaves de calendário de negócios para calendários de negócios, consulte [Configurando Calendários](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars)de Negócios.

Limitar o nome a menos de 53 caracteres. Um nome mais curto ajuda a evitar problemas ao exibir a chave do calendário de negócios nas páginas de Gerenciamento de processos no console de administração.

**ID do usuário:** (Obrigatório) ID de usuário que o usuário usa para fazer logon. A ID de usuário não diferencia maiúsculas de minúsculas e deve ser exclusiva no domínio.

Em domínios corporativos, use um atributo não DN como a ID do usuário, pois o DN de um usuário pode ser alterado se ele for movido para outra parte da organização. Essa configuração depende do servidor de diretório. O valor é `objectGUID` para o Ative Diretory 2003, `nsuniqueID` para o Sun™ One e `guid` para o eDiretory.

Certifique-se de que a ID de usuário seja exclusiva. Não use um que tenha sido atribuído a um usuário excluído.

AEM formulários não podem diferenciar entre contas de usuário que têm IDs de usuário e senhas idênticas, mas pertencem a domínios diferentes. Para evitar esse problema, não crie contas que tenham a mesma ID de usuário em vários domínios.

Ao usar o SQL Server como banco de dados, não é possível criar uma ID de usuário que exceda 255 caracteres.

Ao usar o MySQL, a ID do usuário pode conter caracteres estendidos. No entanto, quando se faz uma comparação entre duas cordas, como abcde e âbcdè, elas são consideradas iguais. Por exemplo, ao sincronizar, se um novo usuário foi adicionado ao banco de dados, uma comparação é feita para verificar se um usuário com a mesma ID de usuário existe no banco de dados. Se o usuário *abcde* já existir no banco de dados quando o novo usuário *âbcdè* for adicionado, a comparação não poderá distinguir entre os dois nomes. Pressupõe-se que o usuário já existe no banco de dados e que o novo usuário seja ignorado e não adicionado.

Evite criar nomes de usuários que comecem com um sinal de número (#). A execução de pesquisas de tarefa não retorna resultados para esses nomes de usuário. (See [Working with tasks](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Senha e Confirmar senha:** Senha que o usuário usa para fazer logon. Deve ter no mínimo oito caracteres. Uma senha não é necessária para um usuário que faz parte de um domínio híbrido.

## Detalhes da visualização sobre um usuário {#view-details-about-a-user}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Especifique as informações para restringir a pesquisa e, na lista Em, selecione Usuários e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. É possível classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do usuário para exibir detalhes sobre o. A página Editar usuário exibe detalhes como abaixo sobre o usuário:

   * Informações gerais de identificação, como nome, email, endereço, domínio e organização
   * Funções atribuídas ao usuário
   * Grupos dos quais o usuário é membro

## Alterar a senha de um usuário local {#change-the-password-for-a-local-user}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Especifique as informações para restringir a pesquisa de um usuário específico e clique em **[!UICONTROL Localizar]**. Os resultados da pesquisa são listados na parte inferior da página. É possível classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do usuário e clique em **[!UICONTROL Alterar senha]**.
1. Digite e confirme a nova senha e clique em **[!UICONTROL OK]**. A senha deve ter no mínimo oito caracteres.

## Editar as propriedades de um usuário {#edit-a-user-s-properties}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Para localizar o usuário que deseja editar, faça as seguintes tarefas:

   * Na caixa **[!UICONTROL Localizar]** , digite os critérios de pesquisa.
   * Na lista **[!UICONTROL Usando]** , selecione **[!UICONTROL Nome]**, **[!UICONTROL Email]** ou ID **** de usuário.
   * Na **[!UICONTROL lista]**, selecione **[!UICONTROL Usuários]**.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.

1. Clique no usuário para editar.
1. Para um usuário que faça parte de um domínio local ou híbrido, na guia **[!UICONTROL Detalhe]** , edite as Configurações **** gerais e as Configurações **[!UICONTROL de]** logon e clique em **[!UICONTROL Salvar]**. Para obter detalhes sobre as configurações, consulte Configurações [](adding-configuring-users.md#user-settings)do usuário. Não é possível editar as configurações gerais e de logon de um usuário que pertence a um domínio corporativo.
1. Para editar as configurações de grupo para o usuário, clique na guia Membros do **[!UICONTROL grupo]** e faça as seguintes tarefas:

   * Clique em **[!UICONTROL Localizar grupo]** e preencha as informações de pesquisa.
   * Para adicionar o usuário a um novo grupo, marque a caixa de seleção do grupo, clique em **[!UICONTROL OK]** e em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >Os usuários locais não podem ser adicionados a grupos de diretórios. No entanto, os usuários do diretório podem ser adicionados a grupos locais.

   * Para remover o usuário de um grupo, marque a caixa de seleção do grupo, clique em **[!UICONTROL Excluir]** e em **[!UICONTROL Salvar]**.


1. Para editar as funções do usuário, clique na guia Atribuições **[!UICONTROL de]** função e faça as seguintes tarefas:

   * Para exibir uma lista de funções, clique em **[!UICONTROL Localizar Funções]**.
   * Para adicionar uma função, marque a caixa de seleção da função, clique em **[!UICONTROL OK]** e, em seguida, clique em **[!UICONTROL Salvar]**.
   * Para remover uma função, marque a caixa de seleção da função, clique em **[!UICONTROL Cancelar atribuição]** e, em seguida, clique em **[!UICONTROL Salvar]**.

## Excluir um usuário {#delete-a-user}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Usuários e grupos]**.
1. Para localizar o usuário a ser excluído, faça as seguintes tarefas:

   * Na caixa **[!UICONTROL Localizar]** , digite os critérios de pesquisa.
   * Na lista **[!UICONTROL Usando]** , selecione **[!UICONTROL Nome]**, **[!UICONTROL Email]** ou ID **** de usuário.
   * Na **[!UICONTROL lista]**, selecione **[!UICONTROL Usuários]**.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em **[!UICONTROL Localizar]**.

1. Marque a caixa de seleção do usuário, clique em **[!UICONTROL Excluir]** e, em seguida, clique em **[!UICONTROL OK]**.

>[!NOTE]
>
>O AEM Forms em JEE também permite que os usuários do complemento de formulários AEM em execução em um OSGi sejam reconhecidos como usuários AEM. Isso é necessário para cenários em que o logon único entre o AEM Forms no JEE e o complemento de formulários AEM em execução em um OSGi é necessário (por exemplo, espaço de trabalho HTML). A operação de exclusão acima mencionada remove um usuário somente da AEM Forms no JEE. O usuário não é excluído do complemento AEM Forms em execução no ambiente OSGi. No entanto, qualquer tentativa de logon feita após a exclusão do usuário (uma tentativa de logon no servidor JEE do complemento AEM Forms ou no complemento AEM Forms no ambiente OSGi) é negada.

## Criar manipulador de erros de logon personalizado {#create-custom-login-error-handler}

Se um usuário sem os formulários AEM obrigatórios e as permissões de CQ, tentar fazer logon nos seguintes aplicativos incorporados ao CQ, o usuário será redirecionado para a página padrão do CQ 404 que contém o rastreamento de erro:

* Solução de gerenciamento de correspondência
* Espaço de trabalho de formulários AEM

   ***observação **: O Flex Workspace está obsoleto para AEM versão de formulários.*

* gerenciador de formulários
* Relatório de processo

O CQ fornece um mecanismo para substituir o manipulador padrão 404 jsp.

Para obter detalhes sobre como personalizar a página de tratamento de erros, consulte [Personalizar páginas mostradas pelo manipulador](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html) de erros na Documentação do Adobe Experience Manager.

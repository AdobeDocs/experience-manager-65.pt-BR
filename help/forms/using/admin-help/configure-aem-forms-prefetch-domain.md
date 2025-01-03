---
title: Configurar formulários AEM para obter previamente informações de domínio
description: Configure formulários AEM para buscar previamente informações de domínio se você tiver um tempo de resposta mais lento devido a grupos profundamente aninhados ou se for membro de vários grupos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Configurar formulários AEM para obter previamente informações de domínio {#configure-aem-forms-to-prefetchdomain-information}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Os usuários podem enfrentar um tempo de resposta mais lento se pertencerem a muitos grupos (por exemplo, 500 ou mais) ou se os grupos estiverem aninhados profundamente (por exemplo, 30 níveis). Se você estiver com esse problema, poderá configurar formulários AEM para buscar previamente informações de determinados domínios.

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração]**.
1. Para exportar a definição de configuração atual para um arquivo, clique em **[!UICONTROL Exportar]** e salve o arquivo de configuração em outro local.
1. Adicione o seguinte nó (marcado em negrito):

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   Neste exemplo, vários domínios são configurados para busca prévia. Os nomes de domínio são separados por uma &quot;/&quot;. Isso é mostrado no exemplo acima com *Nome_Domínio1*, *Nome_Domínio2* e *Nome_Domínio3*.

1. Para importar o arquivo atualizado, no Gerenciamento de Usuários, clique em **[!UICONTROL Configuração > Importar e Exportar Arquivos de Configuração]**.
1. Clique em **[!UICONTROL Procurar]** para localizar o arquivo, clique em Importar e em **[!UICONTROL OK]**.

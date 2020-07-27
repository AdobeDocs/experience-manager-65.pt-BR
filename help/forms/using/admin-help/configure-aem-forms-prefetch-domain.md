---
title: Configurar formulários AEM para pré-buscar informações de domínio
seo-title: Configurar formulários AEM para pré-buscar informações de domínio
description: Configure os formulários do AEM para obter previamente informações de domínio se você tiver um tempo de resposta mais lento devido a grupos profundamente aninhados ou se for membro de muitos grupos.
seo-description: Configure os formulários do AEM para obter previamente informações de domínio se você tiver um tempo de resposta mais lento devido a grupos profundamente aninhados ou se for membro de muitos grupos.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Configurar formulários AEM para pré-buscar informações de domínio {#configure-aem-forms-to-prefetchdomain-information}

Os usuários podem experimentar um tempo de resposta mais lento se pertencerem a muitos grupos (por exemplo, 500 ou mais) ou se os grupos estiverem profundamente aninhados (por exemplo, 30 níveis). Se você estiver enfrentando esse problema, é possível configurar formulários do AEM para obter informações previamente de determinados domínios.

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos]** de configuração.
1. Para exportar a configuração atual para um arquivo, clique em **[!UICONTROL Exportar]** e salve o arquivo de configuração em outro local.
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

   Neste exemplo, vários domínios são configurados para busca prévia. Os nomes de domínio são separados por &quot;/&quot;. Isso é mostrado no exemplo acima com *Domain_Name1*, *Domain_Name2* e *Domain_Name3*.

1. Para importar o arquivo atualizado, em Gerenciamento de usuários, clique em **[!UICONTROL Configuração > Importar e exportar arquivos]** de configuração.
1. Clique em **[!UICONTROL Procurar]** para localizar o arquivo, clique em Importar e em **[!UICONTROL OK]**.


---
title: Atualizar para AEM 6.5 Forms no OSGi
description: Você pode executar uma atualização direta do AEM 6.1 Forms, AEM 6.2 Forms e LiveCycle ES4 SP1 para AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 5%

---

# Atualizar para AEM 6.5 Forms no OSGi {#upgrade-to-aem-forms-osgi}

Você pode fazer uma atualização direta do AEM 6.3 Forms ou AEM 6.4 Forms para AEM 6.5 Forms.

Caminho de atualização direta de **AEM 6.0 Forms, AEM 6.1 Forms** e **AEM 6.2 Forms** para AEM 6.5 Forms não está disponível. Executar uma [atualização para o AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [atualização para o AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)ou [atualização para o AEM 6.4 Forms](/help/forms/using/upgrade.md) e atualize do AEM 6.3 Forms ou AEM 6.4 Forms para AEM 6.5 Forms.

Faça o seguinte para atualizar do AEM 6.3 Forms ou AEM 6.4 Forms para AEM 6.5 Forms:

1. Atualize a instância de AEM existente para AEM 6.5. As etapas estão listadas abaixo:

   1. Instale o service pack e os patches mais recentes para o AEM 6.3 Forms ou AEM 6.4 Forms. Para obter detalhes, consulte [Hub de AEM](https://helpx.adobe.com/br/experience-manager/aem-releases-updates.html).
   1. Prepare a instância de origem para a atualização. Para obter etapas detalhadas, consulte [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Baixe o [Início rápido do AEM 6.5](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Somente instalações baseadas em Unix/Linux)** Se você estiver usando UNIX ou Linux como o sistema operacional subjacente, abra a janela do terminal, navegue até a pasta que contém crx-quickstart e execute o seguinte comando:

      `chmod -R 755 ../crx-quickstart`

   1. Atualize sua instância do AEM para AEM 6.3. Para obter instruções passo a passo, consulte [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md).

      Antes de continuar com as próximas etapas, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no &lt;crx-repository>/error.log .

      >[!NOTE]
      >
      >Depois que o servidor estiver funcionando, alguns pacotes do AEM Forms permanecerão no estado de instalação. O número de pacotes pode variar para cada instalação. Você pode ignorar com segurança o estado desses pacotes. Os pacotes estão listados em https://&#39;[server]:[porta]&#39;/system/console/.

1. Instale o pacote complementar do AEM Forms. As etapas estão listadas abaixo:

   1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
   1. Clique em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
   1. No **[!UICONTROL Filtros]** seção:
      1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
      1. Selecione a versão e o tipo do pacote. Também é possível usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
   1. Toque no nome do pacote aplicável ao seu sistema operacional e selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Baixar]**.
   1. Abra [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR) e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote.
   1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

      Você também pode baixar o pacote usando o link direto listado em [Versões do AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) artigo 10. o

      >[!NOTE]
      >
      >Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não pare imediatamente o servidor.** Antes de parar o servidor do AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no &lt;crx-repository>/error.log e o log é estável. Observe também que alguns pacotes podem permanecer no estado instalado. Você pode ignorar com segurança o estado desses pacotes.

1. Reinicie a instância de AEM.

1. Execute atividades pós-instalação.

   * **Executar Utilitário de Migração**

      O utilitário de migração torna os ativos de gerenciamento de correspondência e formulários adaptáveis das versões anteriores compatíveis com AEM formulários 6.5. Você pode baixar o utilitário da Distribuição de software AEM. Para obter informações passo a passo sobre como configurar e usar o utilitário de migração, consulte [utilitário de migração](../../forms/using/migration-utility.md).

      Se estiver usando [Amostra para integrar componentes de rascunhos e envios](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) com o banco de dados e atualizando de uma versão anterior, execute as seguintes consultas SQL após executar a atualização:

      ```sql
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```sql
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(Se estiver atualizando do AEM 6.2 Forms ou versões anteriores apenas) Reconfigure o Adobe Sign**

      Se tiver o Adobe Sign configurado na versão anterior do AEM Forms, reconfigure o Adobe Sign a partir dos serviços da AEM Cloud. Para obter mais detalhes, consulte [Integrar o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Suporte para jQuery**

      No AEM 6.5 Forms, a versão do jQuery é atualizada para 3.2.1 e a versão da interface do usuário do jQuery é atualizada para 1.12.1. AEM Formulário usa o JQuery no **noConflict** modo. Portanto, se estiver usando qualquer outra versão do jQuery, nenhum problema será exibido durante a execução de uma atualização. No entanto, ao atualizar para o AEM 6.5 Forms:

      * Certifique-se de que seus componentes personalizados, se houver, sejam compatíveis com as versões do jQuery compatíveis.
      * Remova as APIs não compatíveis dos componentes personalizados. Consulte [guia de atualização](https://jquery.com/upgrade-guide/3.0/) para obter a lista de APIs removidas. Por exemplo, o suporte para as APIs load(), .unload() e .error() é removido. Use o método .on() no lugar das APIs acima. Por exemplo, altere $(&quot;img&quot;).load(fn) para $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(Se estiver atualizando do AEM 6.2 Forms ou versões anteriores somente) Reconfigure análises e relatórios**

      No AEM 6.4 Forms, a variável de tráfego para origem e evento bem-sucedido para impressão não estão disponíveis. Portanto, quando você atualiza do AEM 6.2 Forms ou versões anteriores, o AEM Forms para de enviar dados para o servidor Adobe Analytics e os relatórios de análise para formulários adaptáveis não estão disponíveis. Além disso, o AEM 6.4 Forms apresenta variáveis de tráfego para a versão de análise de formulário e evento bem-sucedido pela quantidade de tempo gasto em um campo. Assim, reconfigure análises e relatórios para o seu ambiente AEM Forms. Para obter etapas detalhadas, consulte [Configuração de análises e relatórios](../../forms/using/configure-analytics-forms-documents.md).


1. Verifique se o servidor foi atualizado com êxito, se todos os dados também foram migrados com êxito e se podem operar normalmente.

   * **Verifique o status dos pacotes:** Certifique-se de que todos os pacotes estejam no estado ativo.
   * **Verificar replicação e replicação inversa:** Publique, preencha e envie alguns formulários migrados. Verifique também os dados enviados.
   * **Verifique o acesso às interfaces de usuário do administrador e desenvolvedor:** Faça logon AEM instância em uma conta de administrador e verifique se você tem acesso aos seguintes URLs:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   No AEM 6.4 Forms, a estrutura do repositório crx foi alterada. Se você atualizar do 6.3 Forms para o AEM 6.5 Forms, use os caminhos alterados para a personalização que você cria novamente. Para obter a lista completa de caminhos alterados, consulte [Reestruturação do repositório Forms no AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).

---
title: Atualização para o AEM 6.5 Forms
seo-title: Atualização para o AEM 6.5 Forms
description: Você pode fazer uma atualização direta do AEM 6.1 Forms, AEM 6.2 Forms e do LiveCycle ES4 SP1 para AEM 6.3 Forms.
seo-description: Você pode fazer uma atualização direta do AEM 6.1 Forms, AEM 6.2 Forms e do LiveCycle ES4 SP1 para AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# Atualize para o AEM 6.5 Forms no OSGi {#upgrade-to-aem-forms-osgi}

Você pode fazer uma atualização direta do AEM 6.3 Forms ou AEM 6.4 Forms para AEM 6.5 Forms.

O caminho de atualização direta de **AEM 6.0 Forms, AEM 6.1 Forms** e **AEM 6.2 Forms** para AEM 6.5 Forms não está disponível. Faça uma atualização intermediária [para AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [atualize para AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html) ou [atualize para AEM 6.4 Forms](/help/forms/using/upgrade.md) e, em seguida, atualize de AEM 6.3 Forms ou AEM 6.4 Forms para AEM 6.5 Forms.

Faça o seguinte para atualizar do AEM 6.3 Forms ou AEM 6.4 Forms para o AEM 6.5 Forms:

1. Atualize a instância AEM existente para AEM 6.5. As etapas estão listadas abaixo:

   1. Instale o service pack e os patches mais recentes para AEM 6.3 Forms ou AEM 6.4 Forms. Para obter detalhes, consulte [AEM Sustenance Hub](https://helpx.adobe.com/br/experience-manager/aem-releases-updates.html).
   1. Prepare a instância de origem para a atualização. Para obter etapas detalhadas, consulte [Atualizando para AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Baixe o [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Somente instalações baseadas em Unix/Linux)** Se você estiver usando UNIX ou Linux como o sistema operacional subjacente, abra a janela do terminal, navegue até a pasta que contém crx-quickstart e execute o seguinte comando:

      `chmod -R 755 ../crx-quickstart`

   1. Atualize sua instância AEM para AEM 6.3. Para obter instruções passo a passo, consulte [Atualizando para AEM 6.5](/help/sites-deploying/upgrade.md).

      Antes de continuar com as próximas etapas, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no arquivo &lt;crx-repository>/error.log.

      >[!NOTE]
      >
      >Depois que o servidor estiver funcionando, alguns pacotes da AEM Forms permanecerão no estado de instalação. O número de pacotes pode variar para cada instalação. É possível ignorar com segurança o estado desses pacotes. Os pacotes estão listados em https://&#39;[server]:[port]&#39;/system/console/.

1. Instale o pacote suplementar do AEM Forms. As etapas estão listadas abaixo:

   1. Abra [Distribuição de software](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Software Distribution (Distribuição de software).
   1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
   1. Na seção **[!UICONTROL Filtros]**:
      1. Selecione **[!UICONTROL Forms]** na lista suspensa **[!UICONTROL Solution]**.
      1. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
   1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Download]**.
   1. Abra [Gerenciador de pacotes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
   1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

      Você também pode baixar o pacote usando o link direto listado no artigo [Versões da AEM Forms](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html).

      >[!NOTE]
      >
      >Depois que o pacote for instalado, você será solicitado a reiniciar a instância AEM. **Não interrompa imediatamente o servidor.** Antes de parar o servidor AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no arquivo  &lt;crx-repository>/error.log e o log esteja estável. Observe também que alguns pacotes podem permanecer no estado instalado. É possível ignorar com segurança o estado desses pacotes.

1. Reinicie a instância AEM.

1. Execute atividades pós-instalação.

   * **Executar utilitário de migração**

      O utilitário de migração torna os formulários adaptáveis e os ativos de gerenciamento de correspondência das versões anteriores compatíveis com os formulários AEM 6.5. Você pode fazer o download do utilitário AEM Distribuição de software. Para obter informações detalhadas sobre como configurar e usar o utilitário de migração, consulte [utilitário de migração](../../forms/using/migration-utility.md).

      Se você estiver usando [Amostra para integrar os rascunhos e o componente de submissão](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) ao banco de dados e atualizar de uma versão anterior, execute os seguintes query SQL após executar a atualização:

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

      Se você tiver o Adobe Sign configurado na versão anterior do AEM Forms, reconfigure o Adobe Sign dos serviços da AEM Cloud. Para obter mais detalhes, consulte [Integrar o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Suporte para jQuery**

      No AEM 6.5 Forms, a versão do jQuery é atualizada para 3.2.1 e a versão da interface do usuário do jQuery é atualizada para 1.12.1. AEM formulário usa JQuery no modo **noConflict**. Portanto, se você estiver usando qualquer outra versão do jQuery, nenhum problema será exibido ao executar uma atualização. No entanto, ao atualizar para o AEM 6.5 Forms:

      * Certifique-se de que seus componentes personalizados, se houver, sejam compatíveis com as versões do jQuery suportadas.
      * Remova as APIs não compatíveis dos componentes personalizados. Consulte [guia de atualização](https://jquery.com/upgrade-guide/3.0/) para obter a lista de APIs removidas. Por exemplo, o suporte para as APIs load(), .unload() e .error() é removido. Use o método .on() no lugar das APIs acima. Por exemplo, altere $(&quot;img&quot;).load(fn) para $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(Se estiver atualizando do AEM 6.2 Forms ou versões anteriores apenas) Reconfigure análises e relatórios**

      No AEM 6.4 Forms, a variável de tráfego para o evento de origem e sucesso para impressão não está disponível. Portanto, ao atualizar do AEM 6.2 Forms ou versões anteriores, a AEM Forms deixa de enviar dados para o servidor Adobe Analytics e os relatórios de análise para formulários adaptáveis não estão disponíveis. Além disso, a AEM 6.4 Forms apresenta uma variável de tráfego para a versão de análise de formulário e evento bem-sucedido pelo tempo gasto em um campo. Portanto, reconfigure as análises e os relatórios do seu ambiente AEM Forms. Para obter etapas detalhadas, consulte [Configuração de análises e relatórios](../../forms/using/configure-analytics-forms-documents.md).


1. Verifique se o servidor foi atualizado com êxito, se todos os dados também foram migrados com êxito e se podem funcionar normalmente.

   * **Verifique o status dos pacotes:** verifique se todos os pacotes estão no estado ativo.
   * **Verificar replicação e replicação reversa:** Publicar, preencher e enviar alguns formulários migrados. Verifique também os dados enviados.
   * **Verifique o acesso às interfaces de usuário do administrador e desenvolvedor:** faça logon AEM instância de uma conta de administrador e verifique se você tem acesso aos seguintes URLs:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   No AEM 6.4 Forms, a estrutura do repositório crx foi alterada. Se você atualizar do Forms 6.3 para o Forms AEM 6.5, use os caminhos alterados para a personalização que você cria novamente. Para obter a lista completa dos caminhos alterados, consulte [Reestruturação do repositório Forms em AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).


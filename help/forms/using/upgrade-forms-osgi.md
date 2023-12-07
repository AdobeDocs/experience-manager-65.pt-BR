---
title: Atualização para AEM 6.5 Forms no OSGi
description: Você pode executar uma atualização direta do AEM 6.1 Forms, AEM 6.2 Forms e LiveCycle AEM ES4 SP1 para o 6.3 Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# Atualização para AEM 6.5 Forms no OSGi {#upgrade-to-aem-forms-osgi}

Você pode realizar uma atualização direta do AEM 6.3 Forms ou do AEM 6.4 Forms AEM para o 6.5 Forms.

Caminho de atualização direto de **AEM 6.0 Forms, AEM 6.1 Forms**, e **AEM 6.2 Forms** para AEM 6.5, o Forms não está disponível. Executar um intermediário [atualização para o AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [atualização para o AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)ou [atualização para o AEM 6.4 Forms](/help/forms/using/upgrade.md) e, em seguida, atualize do AEM 6.3 Forms, ou AEM 6.4 Forms para o AEM 6.5 Forms.

Faça o seguinte para atualizar do AEM 6.3 Forms ou do AEM 6.4 Forms AEM para o 6.5 Forms:

1. Atualize a instância existente do AEM para AEM 6.5. As etapas estão listadas abaixo:

   1. Instale o service pack e os patches mais recentes do AEM 6.3 Forms ou AEM 6.4 Forms. Para obter detalhes, consulte [Hub de sustentação do AEM](https://helpx.adobe.com/br/experience-manager/aem-releases-updates.html).
   1. Prepare a instância de origem para a atualização. Para obter etapas detalhadas, consulte [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Baixe o [QuickStart do AEM 6.5](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Somente instalações baseadas em Unix/Linux)** Se você estiver usando UNIX ou Linux como o sistema operacional subjacente, abra a janela do terminal, navegue até a pasta que contém crx-quickstart e execute o seguinte comando:

      `chmod -R 755 ../crx-quickstart`

   1. Atualize sua instância do AEM para AEM 6.3. Para obter instruções passo a passo, consulte [Atualização para o AEM 6.5](/help/sites-deploying/upgrade.md).

      Antes de continuar com as próximas etapas, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no &lt;crx-repository>arquivo /error.log.

      >[!NOTE]
      >
      >Depois que o servidor estiver em funcionamento, alguns pacotes do AEM Forms permanecerão no estado de instalação. O número de pacotes pode variar para cada instalação. Você pode ignorar com segurança o estado desses pacotes. Os pacotes estão listados em https://&#39;[server]:[porta]&quot;/system/console/.

1. Instale o pacote complementar do AEM Forms. As etapas estão listadas abaixo:

   1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
   1. Selecionar **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
   1. No **[!UICONTROL Filtros]** seção:
      1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
      1. Selecione a versão e o tipo do pacote. Você também pode usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
   1. Selecione o nome do pacote aplicável ao seu sistema operacional e **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
   1. Abertura [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e clique em **[!UICONTROL Fazer upload do pacote]** para carregar o pacote.
   1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

      Também é possível baixar o pacote usando o link direto listado em [Versões do AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) artigo.

      >[!NOTE]
      >
      >Após a instalação do pacote, você será solicitado a reiniciar a instância do AEM. **Não pare imediatamente o servidor.** Antes de interromper o servidor do AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no &lt;crx-repository>/error.log e o log é estável. Observe também que alguns pacotes podem permanecer no estado instalado. Você pode ignorar com segurança o estado desses pacotes.

1. Reinicie a instância do AEM.

1. Executar atividades de pós-instalação.

   * **Executar utilitário de migração**

     O utilitário de migração torna os formulários adaptáveis e os ativos de gerenciamento de correspondência das versões anteriores compatíveis com formulários AEM 6.5. Você pode baixar o utilitário da Distribuição de software AEM. Para obter informações detalhadas sobre como configurar e usar o utilitário de migração, consulte [utilitário de migração](../../forms/using/migration-utility.md).

     Se você estiver usando [Amostra para integrar o componente de rascunhos e envios](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) com o banco de dados e fazendo upgrade de uma versão anterior, execute as seguintes consultas SQL após executar o upgrade:

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

   * **(Se estiver atualizando do AEM 6.2 Forms ou de versões anteriores somente) Reconfigure o Adobe Sign**

     Se você tiver o Adobe Sign configurado na versão anterior do AEM Forms, reconfigure o Adobe Sign a partir dos serviços em nuvem do AEM. Para obter mais detalhes, consulte [Integrar o Adobe Sign com o AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Suporte para jQuery**

     No AEM 6.5 Forms, a versão do jQuery é atualizada para 3.2.1 e a versão da interface do usuário do jQuery é atualizada para 1.12.1. O formulário AEM usa JQuery no **noConflict** modo. Portanto, se você estiver usando qualquer outra versão do jQuery, nenhum problema será exibido ao executar um upgrade. No entanto, ao atualizar para o AEM 6.5 Forms:

      * Certifique-se de que os componentes personalizados, se houver, sejam compatíveis com as versões do jQuery compatíveis.
      * Remova APIs não compatíveis dos componentes personalizados. Consulte [guia de atualização](https://jquery.com/upgrade-guide/3.0/) para obter a lista de APIs removidas. Por exemplo, o suporte para as APIs load(), .unload() e .error() é removido. Use o método .on() no lugar das APIs mencionadas anteriormente. Por exemplo, altere $(&quot;img&quot;).load(fn) para $(&quot;img&quot;).on(&quot;load&quot;, fn).

   * **(Se estiver atualizando do AEM 6.2 Forms ou de versões anteriores somente) Reconfigure o Analytics e os relatórios**

     No AEM 6.4 Forms, a variável de tráfego para origem e o evento bem-sucedido para impressão não estão disponíveis. Assim, ao atualizar do AEM 6.2 Forms ou de versões anteriores, o AEM Forms interrompe o envio de dados para o servidor do Adobe Analytics e os relatórios do Analytics para formulários adaptáveis não estão disponíveis. Além disso, o AEM 6.4 Forms introduz a variável de tráfego para a versão da análise de formulário e evento de sucesso para o tempo gasto em um campo. Portanto, reconfigure as análises e os relatórios para o ambiente do AEM Forms. Para obter etapas detalhadas, consulte [Configuração de análises e relatórios](../../forms/using/configure-analytics-forms-documents.md).

1. Verifique se o servidor foi atualizado com êxito, se todos os dados também foram migrados com êxito e se ele pode funcionar normalmente.

   * **Verifique o status dos pacotes:** Verifique se todos os pacotes estão no estado ativo.
   * **Verifique a replicação e a replicação inversa:** Publicar, preencher e enviar alguns formulários migrados. Verifique também os dados enviados.
   * **Verifique o acesso às interfaces de usuário do administrador e do desenvolvedor:** Faça logon na instância do AEM com uma conta de administrador e verifique se você tem acesso aos seguintes URLs:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   No AEM 6.4 Forms, a estrutura do repositório crx mudou. Se você atualizar do Forms 6.3 para o AEM 6.5 Forms, use os caminhos alterados para a personalização que você cria novamente. Para obter a lista completa de caminhos alterados, consulte [Reestruturação do repositório Forms no AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).

---
title: Usar ativos conectados para compartilhar ativos DAM no fluxo de trabalho de criação do Adobe Experience Manager Sites
description: Use os ativos disponíveis em uma implantação remota dos ativos Adobe Experience Manager ao criar suas páginas da Web em outra implantação do Site do Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c4e6e74e091fe64b0a936b3f1bf95db7b6185956

---


# Usar ativos conectados para compartilhar ativos DAM em sites AEM {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Em grandes empresas, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de sites e os ativos digitais usados para criar esses sites podem residir em diferentes implantações. Algumas razões podem ser implantações geograficamente distribuídas, necessárias para trabalhar em paralelo; aquisições que conduzam a infraestruturas heterogêneas que a empresa-mãe pretende consolidar; crescimento que leva a tal escala que é necessária uma instância dedicada para o gerenciamento de ativos.

O AEM Sites oferece recursos para criar páginas da Web e o AEM Assets é o sistema de gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites. O AEM agora dá suporte ao caso de uso acima integrando o AEM Sites e o AEM Assets.

## Visão geral dos ativos conectados {#overview-of-connected-assets}

Ao editar páginas no Editor de páginas, os autores podem pesquisar, navegar e incorporar facilmente ativos de uma implantação diferente do AEM Assets. Para fazer um administrador do AEM, faça uma integração única de uma implantação local do AEM Sites com uma implantação diferente (remota) dos ativos AEM.

Para os autores do Sites, os ativos remotos estão disponíveis como ativos locais somente leitura. A funcionalidade suporta pesquisa e uso ininterruptos de alguns ativos remotos de cada vez. Para disponibilizar muitos ativos remotos em uma única implantação local, considere migrar os ativos em massa. Consulte Guia [de migração de](/help/assets/assets-migration-guide.md)ativos.

### Pré-requisitos e implantações compatíveis {#prerequisites}

Antes de usar ou configurar esse recurso, verifique o seguinte:

* Os usuários fazem parte de grupos de usuários apropriados em cada implantação.
* Para os tipos de implantação do Adobe Experience Manager, um dos critérios suportados é atendido. Os ativos AEM 6.5 funcionam com o AEM como um serviço em nuvem. Para obter mais informações, consulte Funcionalidade de ativos [conectados no AEM como um serviço](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)em nuvem.

   |  | AEM Sites as a Cloud Service | AEM 6.5 Sites no AMS | Sites do AEM 6.5 no local |
   |---|---|---|---|
   | **AEM Assets as a Cloud Service** | Suportado | Suportado | Suportado |
   | **AEM 6.5 Assets no AMS** | Suportado | Suportado | Suportado |
   | **Ativos no local do AEM 6.5** | Não suportado | Não suportado | Não suportado |

### Formatos de arquivo não suportados {#mimetypes}

Os autores podem pesquisar por imagens e os seguintes tipos de documentos no Localizador de conteúdo e usar os ativos pesquisados no Editor de páginas. Os documentos podem ser adicionados ao `Download` componente e as imagens podem ser adicionadas ao `Image` componente. Os autores também podem adicionar os ativos remotos em qualquer componente AEM personalizado que estende os componentes padrão `Download` ou `Image` . A lista de formatos suportados é:

* **Formatos** de imagem: Os formatos de imagem suportados pelo componente [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html) Imagem são suportados pelos Ativos conectados. Os Componentes de Dynamic Media não são suportados.
* **Formatos** de documento: Consulte Formatos [de documento compatíveis com os ativos](assets-formats.md#supported-document-formats)conectados.

### Users and groups involved {#users-and-groups-involved}

As várias funções envolvidas para configurar e usar o recurso e seus grupos de usuários correspondentes são descritas abaixo. O escopo local é usado para o caso de uso em que uma página da Web é criada por um autor. O escopo remoto é usado para a implantação do DAM que hospeda os ativos necessários. O autor do Sites busca esses ativos remotos.

| Função | Escopo | Grupo de usuários | Nome do usuário no caminho | Requisito |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Administrador do AEM Sites | Local | Administrador do AEM | `admin` | Configure o AEM, configure a integração com a implantação remota de Ativos. |
| Usuário DAM | Local | Autor | `ksaner` | Usado para exibir e duplicar os ativos obtidos em `/content/DAM/connectedassets/`. |
| Autor do AEM Sites | Local | Autor (com acesso de leitura no DAM remoto e acesso de autor em sites locais) | `ksaner` | Os usuários finais são autores do Sites que usam essa integração para melhorar sua velocidade de conteúdo. Os autores pesquisam e navegam por ativos no DAM remoto usando o Localizador de conteúdo e usando as imagens necessárias em páginas da Web locais. As credenciais do usuário `ksaner` DAM são usadas. |
| Administrador do AEM Assets | Remoto | Administrador do AEM | `admin` no AEM remoto | Configure o CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos de várias origens). |
| Usuário DAM | Remoto | Autor | `ksaner` no AEM remoto | Função de autor na implantação remota do AEM. Pesquise e procure ativos em Ativos conectados usando o Localizador de conteúdo. |
| Distribuidor DAM (usuário técnico) | Remoto | construtores de pacotes e autores de sites | `ksaner` no AEM remoto | Esse usuário presente na implantação remota é usado pelo servidor local do AEM (não pela função de autor do site) para buscar os ativos remotos, em nome do autor do Sites. Essa função não é igual às duas `ksaner` funções acima e pertence a um grupo de usuários diferente. |

## Configurar uma conexão entre implantações de Sites e Ativos {#configure-a-connection-between-sites-and-assets-deployments}

Um administrador do AEM pode criar essa integração. Depois de criadas, as permissões necessárias para usá-las são estabelecidas por meio de grupos de usuários definidos na implantação Sites e na implantação do DAM.

Para configurar a conectividade dos ativos conectados e dos sites locais, siga estas etapas.

1. Acesse uma implantação existente do AEM Sites ou crie uma implantação usando o seguinte comando:

   1. Na pasta do arquivo JAR, execute o seguinte comando em um terminal para criar cada servidor AEM.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Após alguns minutos, o servidor AEM é iniciado com êxito. Considere esta implantação do AEM Sites como a máquina local para criação de página da Web, digamos em `https://[local_sites]:4502`.

1. Verifique se os usuários e as funções com escopo local existem na implantação do AEM Sites e na implantação do AEM Assets no AMS. Crie um usuário técnico na implantação do Assets e adicione-o ao grupo de usuários mencionado nos [usuários e grupos envolvidos](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acesse a implantação local do AEM Sites em `https://[local_sites]:4502`. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Configuração **[!UICONTROL de ativos]** conectados e forneça os seguintes valores:

   1. O local dos ativos AEM é `https://[assets_servername_ams]:[port]`.
   1. Credenciais de um distribuidor DAM (usuário técnico).
   1. No campo **[!UICONTROL Ponto]** de montagem, insira o caminho AEM local onde o AEM busca os ativos. Por exemplo, `remoteassets` pasta.

   1. Ajuste os valores do Limite **[!UICONTROL de otimização da transferência binária]** original, dependendo da sua rede. Uma representação de ativo com um tamanho maior que esse limite é transferida de forma assíncrona.
   1. Selecione **[!UICONTROL Armazenamento de dados compartilhado com ativos]** conectados se você usar um armazenamento de dados para armazenar seus ativos e o armazenamento de dados for o armazenamento comum entre as duas implantações do AEM. Nesse caso, o limite não importa, pois os binários de ativos reais residem no armazenamento de dados e não são transferidos.
   ![Uma configuração típica para ativos conectados](assets/connected-assets-typical-config.png)

   *Figura: Uma configuração típica para ativos conectados*

1. Como os ativos já são processados e as execuções são buscadas, desative os inicializadores do fluxo de trabalho. Ajuste as configurações do iniciador na implantação local (Sites AEM) para excluir a `connectedassets` pasta, na qual os ativos remotos são buscados.

   1. Na implantação do AEM Sites, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Iniciadores]**.

   1. Procure por Iniciadores com fluxos de trabalho como Ativo **[!UICONTROL de atualização do]** DAM e Writeback **[!UICONTROL de metadados do]** DAM.

   1. Selecione o iniciador do fluxo de trabalho e clique em **[!UICONTROL Propriedades]** na barra de ações.

   1. No assistente Propriedades, altere os campos **[!UICONTROL Caminho]** como os seguintes mapeamentos para atualizar suas expressões regulares para excluir os ativos **[!UICONTROL conectados]** do ponto de montagem.
   | Antes | Depois |
   |---|---|
   | /content/dam(/((?!/subassets).)*/)representações/originais | /content/dam(/((?!/subassets)(?!connectedassets).)*/)representações/originais |
   | /content/dam(/.*/)representações/originais | /content/dam(/(?!connectedassets).)*/)representações/originais |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/(?!connectedassets).)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >Todas as execuções que estão disponíveis na implantação remota do AEM são buscadas, quando os autores buscam um ativo. Se você quiser criar mais representações de um ativo buscado, pule esta etapa de configuração. O fluxo de trabalho do Ativo de atualização do DAM é acionado e cria mais execuções. Essas execuções estão disponíveis somente na implantação local de Sites e não na implantação remota de DAM.

1. Adicione a instância do AEM Sites como uma das Origens **** permitidas na configuração remota do CORS do AEM Assets.

   1. Faça logon usando as credenciais de administrador. Procure por Origem Cruzada. Acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da Web]**.

   1. Para criar uma configuração de CORS para a instância do AEM Sites, clique no ícone ![aem_assets_add_icon](assets/aem_assets_add_icon.png) ao lado da Política **[!UICONTROL de compartilhamento de recursos entre origens do]** Adobe Granite.

   1. No campo Origens **[!UICONTROL permitidas]**, insira o URL dos Sites locais, ou seja, `https://[local_sites]:[port]`. Salve a configuração.

## Usar ativos remotos {#use-remote-assets}

Os autores do site usam o Content Finder para se conectar à instância do DAM. Os autores podem procurar e arrastar os ativos remotos em um componente. Para autenticar no DAM remoto, mantenha as credenciais do usuário DAM fornecidas pelo administrador acessíveis.

Os autores podem usar os ativos disponíveis em ambas as instâncias, DAM local e DAM remoto, em uma única página da Web. Use o Localizador de conteúdo para alternar entre a pesquisa no DAM local ou a pesquisa no DAM remoto.

Somente as tags de ativos remotos que têm uma tag correspondente exata — com a mesma hierarquia de taxonomia — estão disponíveis na instância de Sites local. Quaisquer outras tags são descartadas. Os autores podem pesquisar ativos remotos usando todas as tags presentes na implantação remota do AEM, já que o AEM oferece uma pesquisa em texto completo.

### Progresso do uso {#walk-through-of-usage}

Use a configuração acima para tentar a experiência de criação para entender como a funcionalidade funciona. Use documentos ou imagens de sua escolha na implantação remota do DAM.

1. Navegue até a interface do usuário Ativos na implantação remota acessando **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]** da área de trabalho do AEM. Como alternativa, acesse `https://[assets_servername_ams]:[port]/assets.html/content/dam` em um navegador. Carregue os ativos de sua escolha.
1. Na instância Sites, no ativador de perfil no canto superior direito, clique em **[!UICONTROL Representar como]**. Forneça `ksaner` como nome de usuário, selecione a opção fornecida e clique em **[!UICONTROL OK]**.
1. Abra uma página do Web site We.Retail em **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Edite a página. Como alternativa, acesse `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` um navegador para editar uma página.

   Clique em **[!UICONTROL Alternar painel]** lateral no canto superior esquerdo da página.

1. Abra a guia Ativos e clique em **[!UICONTROL Fazer logon nos ativos]** conectados.
1. Forneça as credenciais — `ksaner` como nome de usuário e `password` senha. Esse usuário tem permissões de criação em ambas as implantações do AEM.
1. Procure o ativo que você adicionou ao DAM. Os ativos remotos são exibidos no painel esquerdo. Filtre por imagens ou documentos e filtre ainda mais por tipos de documentos suportados. Arraste as imagens em um `Image` componente e documentos em um `Download` componente.

   Os ativos buscados são somente leitura na implantação local do AEM Sites. Você ainda pode usar as opções fornecidas pelos componentes do AEM Sites para editar o ativo obtido. A edição por componentes não é destrutiva.

   ![Opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: Opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto*

1. Um autor do site é notificado se um ativo é obtido de forma assíncrona e se alguma tarefa de busca falhar. Durante a criação ou mesmo após a criação, os autores podem ver informações detalhadas sobre tarefas de busca e erros na interface do usuário do [async jobs](/help/assets/asynchronous-jobs.md) .

   ![Notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: Notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.*

1. Ao publicar uma página, o AEM exibe uma lista completa de ativos que são usados na página. Certifique-se de que os ativos remotos sejam buscados com êxito no momento da publicação. Para verificar o status de cada ativo obtido, consulte a interface do usuário de trabalhos [assíncronos](/help/assets/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >Mesmo se um ou mais ativos remotos não forem buscados, a página será publicada. O componente que usa o ativo remoto é publicado vazio. A área de notificação do AEM exibe notificações de erros que são exibidos na página de trabalhos assíncronos.

>[!CAUTION]
>
>Uma vez usados em uma página da Web, os ativos remotos buscados são pesquisáveis e utilizáveis por qualquer pessoa que tenha permissões para acessar a pasta local onde os ativos obtidos são armazenados (`connectedassets` na apresentação acima). Os ativos também são pesquisáveis e visíveis no repositório local por meio do [!UICONTROL Content Finder].

Os ativos obtidos podem ser usados como qualquer outro ativo local, exceto que os metadados associados não podem ser editados.

## Limitações   {#limitations}

**Permissões e gerenciamento de ativos**

* Os ativos locais não são sincronizados com os ativos originais na implantação remota. Quaisquer edições, exclusões ou revogação de permissões na implantação do DAM não são propagadas para downstream.
* Os ativos locais são cópias somente leitura. Os componentes do AEM fazem edições não destrutivas em ativos. Nenhuma outra edição é permitida.
* Os ativos obtidos localmente estão disponíveis apenas para fins de criação. Os fluxos de trabalho de atualização de ativos não podem ser aplicados e os metadados não podem ser editados.
* Somente imagens e os formatos de documento listados são suportados. Não há suporte para ativos de Dynamic Media, Fragmentos de conteúdo e Fragmentos de experiência.
* Os esquemas de metadados não são buscados.
* Todos os autores de sites têm permissões de leitura nas cópias buscadas, mesmo que não tenham acesso à implantação remota de DAM.
* Nenhum suporte a API para personalizar a integração.
* A funcionalidade oferece suporte à pesquisa e uso contínuos de ativos remotos. Para disponibilizar muitos ativos remotos em uma implantação local, considere migrar os ativos. Consulte Guia [de migração de](assets-migration-guide.md)ativos.
* Não é possível usar um ativo remoto como uma miniatura de página na interface do usuário Propriedades [!UICONTROL da] página. Você pode definir uma miniatura de uma página da Web na interface do usuário Propriedades [!UICONTROL da] página na [!UICONTROL miniatura] clicando em [!UICONTROL Selecionar imagem].

**Configurar e licenciar**

* A implantação do AEM Assets no AMS é compatível.
* O AEM Sites pode se conectar a um único repositório do AEM Assets de cada vez.
* Uma licença dos ativos AEM que funcionam como repositório remoto.
* Uma ou mais licenças do AEM Sites que funcionam como implantação de criação local.

**Uso**

* Somente a funcionalidade suportada é a pesquisa de ativos remotos e a arrastar os ativos remotos na página local para criar conteúdo.
* A operação de busca expira após 5 segundos. Os autores podem ter problemas para buscar ativos, digamos se houver problemas de rede. Os autores podem tentar novamente arrastando o ativo remoto do Localizador [!UICONTROL de] conteúdo para o Editor [!UICONTROL de]páginas.
* Edições simples que não são destrutivas e a edição é suportada pelo componente AEM `Image` , podem ser feitas em ativos obtidos. Os ativos são somente leitura.

## Solução de problemas {#troubleshoot}

Siga estas etapas para solucionar problemas de cenários de erro comuns:

* Se não for possível pesquisar ativos remotos no Localizador de conteúdo, verifique novamente e certifique-se de que as funções e permissões necessárias estão em vigor.
* Um ativo obtido de uma barragem remota pode não ser publicado em uma página da Web pelas seguintes razões: não existe à distância; falta de permissões adequadas para o obter; falha de rede. Verifique se o ativo não foi removido do DAM remoto ou se as permissões não foram alteradas; Assegurar o cumprimento dos requisitos necessários; tente adicionar o ativo novamente à página e publique-o novamente. Verifique a [lista de trabalhos](/help/assets/asynchronous-jobs.md) assíncronos em busca de erros na busca de ativos.

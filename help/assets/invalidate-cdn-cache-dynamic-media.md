---
title: Invalidar o cache CDN por meio do Dynamic Media
description: A invalidação do conteúdo em cache CDN (Content Delivery Network) permite que você atualize rapidamente os ativos entregues pelo Dynamic Media, em vez de aguardar a expiração do cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 6a44c4ac11f2fdf794895c28468c2a600a09b3c0
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 1%

---


# Invalidar o cache CDN por meio do Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Os ativos de Mídia dinâmica são armazenados em cache pelo CDN (Content Delivery Network) para delivery rápido aos seus clientes. No entanto, ao fazer atualizações nesses ativos, você pode desejar que essas alterações entrem em vigor imediatamente em seu site. Limpar ou invalidar o cache de CDN permite que você atualize rapidamente os ativos entregues pelo Dynamic Media. Em vez de esperar que o cache expire usando um valor TTL (Time To Live) (o padrão é 10 horas), você pode enviar uma solicitação da interface do usuário do Dynamic Media para que o cache expire em minutos.

>[!IMPORTANT]
>
>As etapas a seguir se aplicam somente ao modo Dynamic Media - Scene7 no AEM 6.5, Service Pack 6 (AEM 6.5.6) ou posterior. Este recurso de invalidação de CDN também exige que você use o CDN predefinido que é fornecido com AEM Dynamic Media; nenhum outro CDN personalizado é suportado.<br>Se você usar o Dynamic Media no AEM 6.5, Service Pack 5 (AEM 6.5.5) ou anterior, siga as etapas encontradas em [Invalidar o cache CDN por meio do Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)

Consulte também Visão geral do [cache no Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar o conteúdo em cache CDN para ativos de Dynamic Media:**

*Parte 1 de 2: Criando um modelo de Invalidação CDN*

1. No AEM 6.5.6 ou posterior, toque em **[!UICONTROL Ferramentas > Ativos > Invalidação de CDN.]**

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Na página do modelo **[!UICONTROL de Invalidação de]** CDN, execute uma das seguintes opções com base no seu cenário:

   | Cenário | Opção |
   | --- | --- |
   | Já criei um modelo de invalidação CDN no passado usando o Dynamic Media Classic. | O campo de texto **[!UICONTROL Criar modelo]** é preenchido previamente com os dados do modelo. Nesse caso, você pode editar o modelo ou continuar para a próxima etapa. |
   | Preciso criar um modelo. Em que eu entro? | No campo de texto **[!UICONTROL Criar modelo]** , insira um URL de imagem (incluindo predefinições de imagens ou modificadores) que faça referência `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se o modelo contiver apenas `<ID>`, o Dynamic Media preencherá `https://<publishserver_name>/is/image/<company_name>/<ID>` `<publishserver_name>` onde é o nome do Servidor de publicação definido em Configurações gerais no Dynamic Media Classic; o nome `<company_name>` é a raiz de sua empresa associada a essa instância AEM e `<ID>` são os ativos selecionados por meio do seletor de ativos a serem invalidados.<br>Qualquer publicação de predefinições/modificadores `<ID>` é copiada como está na definição do URL.<br>Somente as imagens - isto é, `/is/image` - podem ser formadas automaticamente com base no modelo.<br>Por exemplo, `/is/content/`adicionar ativos como vídeos ou PDFs usando o seletor de ativos não gera URLs automaticamente. Em vez disso, você deve especificar esses ativos no modelo de Invalidação CDN ou pode adicionar manualmente o URL a esses ativos na *Parte 2 de 2: Definindo opções* de Invalidação de CDN.<br>**Exemplos:**<br> neste primeiro exemplo, o modelo de invalidação contém `<ID>` junto com o URL do ativo que tem `/is/content`. Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. O Dynamic Media forma o URL com base nisso, sendo `<ID>` os ativos selecionados por meio do seletor de ativos que você deseja invalidar.<br>Neste segundo exemplo, o modelo de invalidação contém o URL completo do ativo usado nas propriedades da Web com `/is/content` (não dependente do seletor de ativos). Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` onde o backpack é a ID do ativo.<br>Os formatos de ativos compatíveis com o Dynamic Media são elegíveis para invalidação. Os tipos de arquivos de ativos que *não* são suportados para a invalidação de CDN incluem Postscript, Encapsulated Postscript, Adobe Illustrator, Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word e Rich Text Format.<br>Ao criar o modelo, mas certifique-se de prestar atenção à sintaxe e erros de digitação; O Dynamic Media não faz nenhuma validação de modelo.<br>Observe que você deve especificar URLs para os cortes inteligentes de imagem neste modelo de Invalidação de CDN ou no campo de texto **[!UICONTROL Adicionar URL]** na *Parte 2: Definindo opções de Invalidação de CDN.*<br>**Importante:**Cada entrada em um modelo de Invalidação CDN deve estar em sua própria linha.<br>*O exemplo de modelo a seguir serve apenas para fins ilustrativos.* |

   ![Modelo de Invalidação CDN - Criar](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. No canto superior direito da página de modelo **[!UICONTROL de Invalidação de]** CDN, toque em **[!UICONTROL Salvar]** e, em seguida, em **[!UICONTROL OK.]**<br>   *Parte 2 de 2: Definindo opções de invalidação de CDN*
   <br>

1. Em AEM como um Cloud Service, toque em **[!UICONTROL Ferramentas > Ativos > Invalidação de CDN.]**

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Na página Invalidação **[!UICONTROL CDN - Adicionar detalhes]** , selecione os ativos para invalidação CDN.

   ![Invalidação de CDN - Adicionar Detalhes](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se você decidir deixar as opções **[!UICONTROL Invalidar predefinições de imagens associadas a ativos em CDN]** *e* Invalidar com base no modelo **** desmarcadas, o URL base dos ativos selecionados será formado para invalidação. Você deve usar essa organização de opção apenas para imagens.


   | Opção | Descrição |
   | --- | --- |
   | **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** | (Opcional) Ao marcar essa opção, os ativos selecionados e todos os URLs predefinidos de imagem associados são formados automaticamente para a invalidação do cache.<br>Os ativos e seus URLs predefinidos associados são formados automaticamente para invalidação. Essa opção funciona somente para ativos de imagem. |
   | **[!UICONTROL Invalidação com base no modelo]** | (Opcional) Marque essa opção para usar somente o modelo definido para a formação de URL. |
   | **[!UICONTROL Adicionar ativos]** | Use o Seletor de ativos para selecionar ativos que deseja invalidar. Você pode selecionar ativos publicados ou não publicados.<br>O cache no CDN é baseado em URL, não em ativos. Portanto, é necessário que você esteja ciente dos URLs completos que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los ao modelo. Em seguida, você pode selecionar e adicionar esses ativos e invalidar os URLs em uma etapa. <br>Use essa opção em conjunto com as predefinições de imagens associadas ao ativo **[!UICONTROL Invalidar no CDN]**, ou **[!UICONTROL Invalidar com base no modelo]**, ou em ambos. |
   | **[!UICONTROL Adicionar URL]** | Adicione ou cole manualmente caminhos de URL completos em ativos do Dynamic Media cujo cache de CDN você deseja invalidar. Use esta opção se você não tiver criado um Modelo de Invalidação CDN na ***Parte 1 de 2: Criando um modelo*** de Invalidação CDN e tendo apenas alguns ativos para invalidar.<br>**Importante:** Cada URL adicionado deve estar em sua própria linha.<br>Você pode invalidar até 1000 URLs em um determinado momento. Se o número de URLs no campo de texto **[!UICONTROL Adicionar URL]** for maior que 1000, não será possível tocar em **[!UICONTROL Próximo]**. Nesses casos, você deve tocar em **[!UICONTROL X]** à direita de um ativo selecionado ou em um URL adicionado manualmente para excluí-lo da lista de invalidação.<br>Observe que você deve especificar URLs para os cortes inteligentes de imagem no modelo de Invalidação CDN ou neste campo de texto **[!UICONTROL Adicionar URL]** . |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next.]**
1. Na página Invalidação de **[!UICONTROL CDN - Confirmar]** , na caixa lista **[!UICONTROL URLs]** , você verá uma lista de um ou mais URLs gerados a partir do Modelo de Invalidação de CDN criado anteriormente e dos ativos que você acabou de adicionar.

   Por exemplo, usando o exemplo de Modelo de Invalidação CDN que foi mostrado nas etapas anteriores, suponha que você tenha adicionado um único ativo chamado `spinset`. Quando você toca em **[!UICONTROL Ferramentas > Ativos > Invalidação]** de CDN, isso resulta nos cinco seguintes URLs gerados na **[!UICONTROL Invalidação de CDN - Confirmar]** interface do usuário:

   ![Invalidação de CDN - Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessário, toque em **X** à direita de um URL para excluí-lo do processo de invalidação.

1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Enviar]** para iniciar o processo de invalidação de CDN.

## Solução de problemas de erros de invalidação de CDN

Em todos os casos, o lote inteiro é processado para invalidação ou todo o lote falhou.

| Erro | Explicação |
| --- | --- |
| *Falha ao recuperar URL(s) para ativos selecionados.* | Ocorre se qualquer uma das seguintes situações for atendida:<br>- Uma configuração de Dynamic Media não foi encontrada.<br>- Há uma exceção ao recuperar um usuário de serviço através do qual a configuração do Dynamic Media é lida.<br>- O servidor de publicação ou a raiz de empresa usada para formar os URLs está ausente na configuração do Dynamic Media. |
| *Alguns URLs não estão definidos corretamente. Corrija e envie novamente.* | Ocorre se a API de invalidação do cache CDN IPS retornar um erro de que o URL está fazendo referência a uma empresa diferente ou se o URL não é válido de acordo com a validação feita pela API cdnCacheInvalidation IPS. |
| *Falha ao invalidar o cache CDN.* | Ocorre se a solicitação de invalidação do cache CDN falhar por qualquer outro motivo. |
| *Nenhum URL inserido para ser invalidado.* | Ocorre se não houver URLs presentes na página **[!UICONTROL CDN Invalidation - Confirm]** e você tocar em **[!UICONTROL Submit (Enviar).]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->

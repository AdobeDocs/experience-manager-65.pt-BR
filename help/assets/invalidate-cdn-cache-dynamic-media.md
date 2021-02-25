---
title: Como invalidar o cache CDN por meio do Dynamic Media
description: A invalidação do conteúdo em cache CDN (Content Delivery Network) permite que você atualize rapidamente os ativos entregues pela Dynamic Media, em vez de aguardar a expiração do cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 729fbf3a97d3ae3bc91204f8831fd115d9d77f20
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 1%

---


# Invalidando o cache CDN por meio do Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Os ativos da Dynamic Media são armazenados em cache pela CDN (Content Delivery Network, Rede de conteúdo) para obter delivery rápido aos seus clientes. No entanto, quando você faz atualizações nesses ativos, deseja que essas alterações entrem em vigor imediatamente em seu site. Limpar ou invalidar o cache CDN permite atualizar rapidamente os ativos entregues pela Dynamic Media. Em vez de aguardar a expiração do cache usando um valor TTL (Time To Live) (o padrão é dez horas), você pode enviar uma solicitação da Dynamic Media para que o cache expire em minutos.

>[!NOTE]
>
>Os clientes devem usar o CDN fornecido com a Adobe Experience Manager Dynamic Media para se beneficiarem da invalidação do cache do CDN.

>[!IMPORTANT]
>
>As etapas a seguir se aplicam somente ao modo Dynamic Media - Scene7 no Adobe Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) ou posterior. Este recurso de invalidação de CDN também exige que você use o CDN predefinido que é fornecido com o Experience Manager Dynamic Media; nenhum outro CDN personalizado é suportado.<br>Se você usar o Dynamic Media no Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) ou anterior, siga as etapas encontradas em  [Como invalidar o cache de CDN por meio do Dynamic Media Classic.](/help/assets/invalidate-cdn-cache-dm-classic.md)

Consulte também [Visão geral do cache no Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar o conteúdo em cache CDN para ativos Dynamic Media:**

*Parte 1 de 2: Criando um modelo de Invalidação CDN*

1. Na Experience Manager 6.5.6 ou posterior, toque em **[!UICONTROL Ferramentas > Ativos > Invalidação CDN.]**

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Na página **[!UICONTROL Modelo de Invalidação CDN]**, execute uma das seguintes opções com base no seu cenário:

   | Cenário | Opção |
   | --- | --- |
   | Já criei um modelo de invalidação CDN no passado usando o Dynamic Media Classic. | O campo de texto **[!UICONTROL Criar modelo]** é pré-preenchido com os dados do modelo. Nesse caso, você pode editar o modelo ou continuar para a próxima etapa. |
   | Tenho que criar um modelo. Em que eu entro? | No campo de texto **[!UICONTROL Criar modelo]**, digite um URL de imagem (incluindo predefinições ou modificadores de imagem) referenciando `<ID>`, em vez de uma ID de imagem específica como no exemplo a seguir:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se o modelo contiver apenas `<ID>`, a Dynamic Media preencherá `https://<publishserver_name>/is/image/<company_name>/<ID>` onde `<publishserver_name>` é o nome do Servidor de publicação definido em Configurações gerais no Dynamic Media Classic ... O `<company_name>` é o nome da raiz de empresa associada a esta instância de Experience Manager, e `<ID>` são os ativos selecionados por meio do seletor de ativos a serem invalidados.<br>Qualquer postagem de predefinições/modificadores  `<ID>` é copiada como está na definição do URL.<br>Somente as imagens - isto é,  `/is/image` - podem ser formadas automaticamente com base no modelo.<br>Por exemplo,  `/is/content/`adicionar ativos como vídeos ou PDFs usando o seletor de ativos não gera URLs automaticamente. Em vez disso, você deve especificar esses ativos no modelo de Invalidação CDN ou pode adicionar manualmente o URL a esses ativos em *Parte 2 de 2: Definindo opções de invalidação de CDN*.<br>**Exemplos:**<br> neste primeiro exemplo, o modelo de invalidação contém  `<ID>` junto com o URL do ativo que tem  `/is/content`. Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. A Dynamic Media forma o URL com base nesse caminho, sendo `<ID>` os ativos selecionados por meio do seletor de ativos que você deseja invalidar.<br>Neste segundo exemplo, o modelo de invalidação contém o URL completo do ativo usado nas propriedades da Web com  `/is/content` (não dependente do seletor de ativos). Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` onde o backpack é a ID do ativo.<br>Os formatos de ativos compatíveis com o Dynamic Media são elegíveis para invalidação. Os tipos de arquivos de ativos que são *não* suportados para invalidação CDN incluem PostScript®, PostScript® encapsulado, Adobe Illustrator, Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word e Formato Rich Text.<br>Ao criar o modelo, mas certifique-se de prestar atenção à sintaxe e erros de digitação; A Dynamic Media não faz nenhuma validação de modelo.<br>Especifique URLs para os cortes inteligentes de imagem neste modelo de Invalidação CDN ou no campo  **[!UICONTROL Adicionar]** URLtext na  *Parte 2: Definindo opções de Invalidação de CDN.*<br>**Importante:**cada entrada em um modelo de Invalidação CDN deve estar em sua própria linha.<br>*O exemplo de modelo a seguir serve apenas para fins ilustrativos.* |

   ![Modelo de Invalidação CDN - Criar](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. No canto superior direito da página **[!UICONTROL Modelo de Invalidação CDN]**, toque em **[!UICONTROL Guardar]** e, em seguida, toque em **[!UICONTROL OK.]**<br>

   *Parte 2 de 2: Definindo opções de invalidação de CDN*
   <br>

1. No Experience Manager como um Cloud Service, toque em **[!UICONTROL Ferramentas > Ativos > Invalidação CDN.]**

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Na página **[!UICONTROL Invalidação CDN - Adicionar Detalhes]**, selecione os ativos para invalidação CDN.

   ![Invalidação de CDN - Adicionar Detalhes](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se você decidir deixar as opções **[!UICONTROL Invalidar predefinições de imagens associadas a ativos em CDN]** *e* **[!UICONTROL Invalidar com base no modelo]** desmarcadas, o URL base dos ativos selecionados será formado para invalidação. Use essa organização de opção apenas para imagens.


   | Opção | Descrição |
   | --- | --- |
   | **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** | (Opcional) Ao marcar essa opção, os ativos selecionados e todos os URLs predefinidos de imagem associados são formados automaticamente para a invalidação do cache.<br>Os ativos e seus URLs predefinidos associados são formados automaticamente para invalidação. Essa opção funciona somente para ativos de imagem. |
   | **[!UICONTROL Invalidação com base no modelo]** | (Opcional) Marque essa opção para usar somente o modelo definido para a formação de URL. |
   | **[!UICONTROL Adicionar ativos]** | Use o Seletor de ativos para selecionar ativos que deseja invalidar. Você pode selecionar ativos publicados ou não publicados.<br>O cache no CDN é baseado em URL, não em ativos. Portanto, é necessário que você esteja ciente dos URLs completos que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los ao modelo. Em seguida, você pode selecionar e adicionar esses ativos e invalidar os URLs em uma etapa. <br>Use essa opção com predefinições de imagens associadas ao ativo  **[!UICONTROL Invalidar no CDN]**, ou  **[!UICONTROL Invalidar com base no modelo]**, ou ambos. |
   | **[!UICONTROL Adicionar URL]** | Adicione ou cole manualmente caminhos de URL completos em ativos do Dynamic Media cujo cache de CDN você deseja invalidar. Use esta opção se você não tiver criado um Modelo de Invalidação CDN em ***Parte 1 de 2: Criando um modelo de Invalidação CDN*** e tendo apenas alguns ativos para invalidar.<br>**Importante:** cada URL adicionado deve estar em sua própria linha.<br>Você pode invalidar até 1000 URLs em um determinado momento. Se o número de URLs no campo de texto **[!UICONTROL Adicionar URL]** for maior que 1000, não será possível tocar em **[!UICONTROL Próximo]**. Nesses casos, você deve tocar em **[!UICONTROL X]** à direita de um ativo selecionado ou em um URL adicionado manualmente para excluí-lo da lista de invalidação.<br>Especifique URLs para os cortes inteligentes de imagem no modelo de Invalidação CDN ou neste campo  **[!UICONTROL Adicionar]** URLtext. |

1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Próximo.]**
1. Na página **[!UICONTROL Invalidação CDN - Confirmar]**, na caixa de lista **[!UICONTROL URLs]**, você pode ver uma lista de um ou mais URLs gerados a partir do Modelo de Invalidação CDN criado anteriormente e dos ativos que você acabou de adicionar.

   Por exemplo, usando o exemplo de Modelo de Invalidação CDN que foi mostrado nas etapas anteriores, suponha que você tenha adicionado um único ativo chamado `spinset`. Quando você toca em **[!UICONTROL Ferramentas > Ativos > Invalidação CDN]**, isso resulta nos cinco URLs a seguir gerados na **[!UICONTROL Invalidação CDN - Confirmar]** interface do usuário:

   ![Invalidação de CDN - Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessário, toque em **X** à direita de um URL para excluí-lo do processo de invalidação.

1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Enviar]** para iniciar o processo de invalidação de CDN.

## Solução de problemas de erros de invalidação de CDN

Em todos os casos, o lote inteiro é processado para invalidação ou todo o lote falhou.

| Erro | Explicação |
| --- | --- |
| *Falha ao recuperar URLs para ativos selecionados.* | Ocorre se qualquer um dos seguintes cenários for atendido:<br>- Uma configuração do Dynamic Media não foi encontrada.<br>- Há uma exceção ao recuperar um usuário de serviço pelo qual a configuração do Dynamic Media é lida.<br>- O servidor de publicação ou a raiz de empresa usada para formar os URLs está ausente na configuração do Dynamic Media. |
| *Alguns URLs não estão definidos corretamente. Corrija e envie novamente.* | Ocorre se a API de invalidação do cache CDN IPS retornar um erro de que o URL está referindo-se a uma empresa diferente. Ou, se o URL não for válido de acordo com a validação realizada pela API IPS `cdnCacheInvalidation`. |
| *Falha ao invalidar o cache CDN.* | Ocorre se a solicitação de invalidação do cache CDN falhar por qualquer outro motivo. |
| *Nenhum URL inserido para ser invalidado.* | Ocorre se não houver URLs presentes na página **[!UICONTROL Invalidação CDN - Confirmar]** e você tocar em **[!UICONTROL Enviar.]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->

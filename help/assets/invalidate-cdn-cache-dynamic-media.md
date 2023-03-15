---
title: Invalidar o cache da Rede de entrega de conteúdo por meio do Dynamic Media
description: Invalidar o conteúdo em cache do CDN (Content Delivery Network) permite atualizar rapidamente os ativos entregues pela Dynamic Media, em vez de esperar que o cache expire.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
source-git-commit: b61157b0e9afa49ef72150ae0c1703a959d154be
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 2%

---


# Invalidar o cache da CDN por meio do Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Os ativos da Dynamic Media são armazenados em cache pela CDN (Content Delivery Network) para entrega rápida a seus clientes. No entanto, quando você faz atualizações nesses ativos, deseja que essas alterações entrem em vigor imediatamente no seu site. Limpar ou invalidar o cache CDN permite atualizar rapidamente os ativos entregues pelo Dynamic Media. Em vez de esperar que o cache expire usando um valor TTL (Tempo de vida útil) (o padrão é dez horas), você pode enviar uma solicitação do Dynamic Media para que o cache expire em minutos.



>[!IMPORTANT]
>
>As etapas a seguir se aplicam somente ao modo Dynamic Media - Scene7 no Adobe Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) ou posterior. Esse recurso de invalidação de CDN também requer o uso do CDN pronto para uso fornecido com o Adobe Experience Manager - Dynamic Media. Nenhum outro CDN personalizado é compatível com esse recurso.<br>Se você usa o Dynamic Media no Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) ou anterior, siga as etapas encontradas em [Invalidar o cache CDN por meio do Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Para invalidar o conteúdo em cache do CDN para os ativos do Dynamic Media:**

*Parte 1 de 2: Criação de um modelo de Invalidação de CDN*

1. Na Experience Manager 6.5.6 ou posterior, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Invalidação de CDN]**.

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. No **[!UICONTROL Modelo de Invalidação de CDN]** , execute uma das seguintes opções com base no seu cenário:

   | Cenário | Opção |
   | --- | --- |
   | Eu já criei um modelo de invalidação de CDN no passado usando o Dynamic Media Classic. | O **[!UICONTROL Criar modelo]** O campo de texto é preenchido previamente com os dados do modelo. Nesse caso, você pode editar o modelo ou continuar para a próxima etapa. |
   | Eu tenho que criar um template. O que devo digitar? | No **[!UICONTROL Criar modelo]** campo de texto, insira um URL de imagem (incluindo predefinições ou modificadores de imagem) que faça referência a `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se o modelo contiver apenas `<ID>`, em seguida, o Dynamic Media preenche `https://<publishserver_name>/is/image/<company_name>/<ID>` em que `<publishserver_name>` é o nome do Servidor de publicação definido nas Configurações gerais do Dynamic Media Classic. O `<company_name>` é o nome da raiz da sua empresa associada a esta instância do Experience Manager, e `<ID>` é o ativo selecionado por meio do seletor de ativos a ser invalidado.<br>Qualquer publicação de predefinições/modificadores `<ID>` são copiadas como estão na definição do URL.<br>Somente imagens - ou seja, `/is/image` - pode ser formado automaticamente com base no modelo.<br>Para `/is/content/`, adicionar ativos, como vídeos ou PDF, usando o seletor de ativos não gera URLs automaticamente. Em vez disso, você deve especificar esses ativos no modelo de Invalidação CDN ou pode adicionar manualmente o URL a esses ativos em *Parte 2 de 2: Definindo opções de invalidação de CDN*.<br>**Exemplos:**<br> Neste primeiro exemplo, o modelo de invalidação contém `<ID>` junto com o URL do ativo com `/is/content`. Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. O Dynamic Media forma o URL com base nesse caminho, com `<ID>` sendo os ativos selecionados por meio do seletor de ativos que você deseja invalidar.<br>Neste segundo exemplo, o modelo de invalidação contém o URL completo do ativo usado em suas propriedades da Web com `/is/content` (não depende do seletor de ativos). Por exemplo, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` onde backpack é a ID do ativo.<br>Os formatos de ativos compatíveis com o Dynamic Media são elegíveis para invalidação. Tipos de arquivo do ativo *not* são suportados para invalidação de CDN: PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word e Rich Text Format.<br><br>・ Ao criar o modelo, mas certifique-se de prestar atenção à sintaxe e erros de digitação; O Dynamic Media não faz nenhuma validação de modelo.<br>・ O Modelo de Invalidação CDN pode salvar texto até 2500 caracteres.<br>・ Especifique URLs para recortes inteligentes de imagem neste modelo de Invalidação de CDN ou no **[!UICONTROL Adicionar URL]** campo de texto em *Parte 2: Definindo opções de Invalidação de CDN.*<br>・ Cada entrada em um modelo de Invalidação de CDN deve estar em sua própria linha.<br>・ O seguinte exemplo de modelo de Invalidação de CDN é somente para fins de demonstração. |

   ![Modelo de Invalidação CDN - Criar](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >O Modelo de Invalidação CDN pode salvar texto até 2500 caracteres.

1. No canto superior direito do **[!UICONTROL Modelo de Invalidação de CDN]** página, selecione **[!UICONTROL Salvar]**, em seguida selecione **[!UICONTROL OK]**.<br>

   *Parte 2 de 2: Definindo opções de invalidação de CDN*
   <br>

1. Em Experience Manager as a Cloud Service, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Invalidação de CDN]**.

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. No **[!UICONTROL Invalidação de CDN - Adicionar detalhes]** selecione os ativos para invalidação de CDN.

   ![Invalidação de CDN - Adicionar detalhes](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se decidir deixar as opções **[!UICONTROL Invalidar predefinições de imagens associadas a ativos no CDN]** *e* **[!UICONTROL Invalidar com base no modelo]** desmarcada, o URL base dos ativos selecionados é formado para invalidação. Use essa opção de organização somente para imagens.


   | Opção | Descrição |
   | --- | --- |
   | **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** | (Opcional) Ao marcar essa opção, os ativos selecionados e todos os URLs predefinidos de imagens associados são formados automaticamente para invalidação de cache.<br>Os ativos e seus URLs predefinidos associados são formados automaticamente para invalidação. Essa opção funciona somente para ativos de imagem. |
   | **[!UICONTROL Invalidação com base no modelo]** | (Opcional) Marque essa opção para usar somente o modelo definido para a formação de URL. |
   | **[!UICONTROL Adicionar ativos]** | Use o Seletor de ativos para selecionar os ativos que deseja invalidar. Você pode selecionar ativos publicados ou não publicados.<br>O armazenamento em cache na CDN é baseado em URL e não em ativos. Portanto, é necessário que você esteja ciente dos URLs completos que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los ao modelo. Em seguida, você pode selecionar e adicionar esses ativos e invalidar os URLs em uma etapa. <br>Use esta opção com **[!UICONTROL Invalidar predefinições de imagens associadas a ativos no CDN]** ou **[!UICONTROL Invalidação com base no modelo]** ou ambos. |
   | **[!UICONTROL Adicionar URL]** | Adicione ou cole manualmente caminhos de URL completos em ativos do Dynamic Media cujo cache CDN você deseja invalidar. Use esta opção se você não criar um Modelo de Invalidação CDN em ***Parte 1 de 2: Criação de um modelo de Invalidação de CDN*** e ter apenas alguns ativos para invalidar.<br>**Importante:** Cada URL adicionado deve estar em sua própria linha.<br>Você pode invalidar até 1000 URLs em um determinado momento. Se o número de URLs na variável **[!UICONTROL Adicionar URL]** o campo de texto é maior que 1000, você não pode selecionar **[!UICONTROL Próximo]**. Nesses casos, você deve selecionar **[!UICONTROL X]** à direita de um ativo selecionado ou de um URL adicionado manualmente para excluí-lo da lista de invalidação.<br>Especifique URLs para recortes inteligentes de imagem no modelo de Invalidação CDN ou nesta **[!UICONTROL Adicionar URL]** campo de texto. |

1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Próximo]**.
1. No **[!UICONTROL Invalidação de CDN - Confirmar]** na página **[!UICONTROL URLs]** na caixa de listagem, é possível ver uma lista de um ou mais URLs gerados a partir do Modelo de Invalidação CDN criado anteriormente e os ativos que você acabou de adicionar.

   Por exemplo, usando o exemplo de Modelo de Invalidação CDN mostrado nas etapas anteriores, suponhamos que você tenha adicionado um único ativo chamado `spinset`. Ao navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Invalidação de CDN]**, resulta nos cinco URLs gerados a seguir no **[!UICONTROL Invalidação de CDN - Confirmar]** interface do usuário:

   ![Invalidação de CDN - Confirmar](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessário, selecione **X** à direita de um URL para excluí-lo do processo de invalidação.

1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Enviar]** para iniciar o processo de invalidação de CDN.

## Solução de problemas de erros de invalidação de CDN

Em todos os casos, o lote inteiro é processado para invalidação ou o lote inteiro falhou.

| Erro | Explicação |
| --- | --- |
| *Falha ao recuperar URLs para ativos selecionados.* | Ocorre se qualquer uma das seguintes situações for atendida:<br>- Uma configuração do Dynamic Media não foi encontrada.<br>- Há uma exceção ao recuperar um usuário de serviço pelo qual a configuração do Dynamic Media é lida.<br>- O servidor de publicação ou a raiz da empresa usada para formar os URLs está ausente na configuração do Dynamic Media. |
| *Alguns URLs não estão definidos corretamente. Corrija e reenvie.* | Ocorre se a API de invalidação do cache CDN do IPS retornar um erro de que o URL se refere a uma empresa diferente. Ou, se o URL não for válido de acordo com a validação feita pelo IPS `cdnCacheInvalidation` API. |
| *Falha ao invalidar o cache CDN.* | Ocorre se a solicitação de invalidação do cache CDN falhar por qualquer outro motivo. |
| *Nenhum URL inserido para ser invalidado.* | Ocorre se não houver URLs presentes no **[!UICONTROL Invalidação de CDN - Confirmar]** e você selecionar **[!UICONTROL Enviar]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->

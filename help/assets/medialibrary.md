---
title: Usar o Media Library para o gerenciamento básico de ativos digitais
description: '"[!DNL Experience Manager Assets] e Media Library para gerenciamento de ativos."'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 4%

---


# Usar o Media Library para gerenciamento básico de ativos {#manage-assets-using-media-library}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/medialibrary.html?lang=pt-BR) |

[!DNL Adobe Experience Manager] A plataforma fornece diferentes recursos para gerenciar ativos. O Media Library permite que os usuários façam upload de um pequeno número de ativos para o repositório, pesquisem e usem nas páginas da Web e realizem tarefas simples de gerenciamento de ativos nos ativos.

A Media Library é uma solução leve de Gerenciamento de ativos digitais (DAM) que vem complementar com [!DNL Adobe Experience Manager Sites] licença. [!DNL Sites] O é uma oferta do Web Content Management (WCM). O Media Library funciona com todos os recursos do Experience Manager.

[!DNL Adobe Experience Manager Assets] está disponível separadamente para compra. [!DNL Experience Manager Assets] O permite o gerenciamento robusto de ativos por meio de casos de uso corporativos, personalizações de metadados, esquemas, pesquisa e interface do usuário, além do que a Media Library oferece.

## Requisitos de licenciamento {#avail-media-library-license}

Clientes que tenham [!DNL Sites] As licenças estão habilitadas a usar o Media Library. Funciona com todos os componentes de [!DNL Experience Manager].

O Media Library é instalado como parte do Sites. Nenhuma licença ou pacote adicional é necessário além da licença e instalação do Sites.

## [!DNL Assets] versus Media Library {#assets-and-media-library}

O Experience Manager Assets fornece funcionalidade de DAM de nível empresarial. A funcionalidade de ativos é fornecida com [!DNL Experience Manager] numa única embalagem. No entanto, os usuários que não compraram uma licença do Assets não têm direito a usar os recursos avançados do DAM. Somente sem a licença do Assets [Recursos do Media Library](#use-media-library) estão disponíveis.

Se quiser evitar o uso não intencional de [!DNL Assets] recursos que você não licenciou e remova todos os [!DNL Assets]fluxos de trabalho específicos, componentes, taxonomias, opções e o [!DNL Assets] administrador de [!DNL Experience Manager]. Isso evita que os usuários usem acidentalmente [!DNL Assets] recursos que você não licenciou.

## Usar o Media Library {#use-media-library}

O Media Library fornece recursos básicos de DAM para os seguintes casos de uso:

* Páginas da Web criadas usando [!DNL Adobe Experience Manager Sites].
* Formulários adaptáveis e comunicações criados com [!DNL Adobe Experience Manager Forms].
* Experiências em tela digital criadas com o uso de [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] REST APIs HTTP para operações sem periféricos.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Para usar a funcionalidade do Media Library, é possível usar o [!DNL Experience Manager] interface do usuário. A Media Library faz parte do [!DNL Experience Manager Sites] instalação e nenhuma interface ou complemento separado é necessário. Usando a interface existente, os usuários do Media Library têm direito a realizar as seguintes tarefas:

* Crie pastas para organizar ativos.
* Fazer upload de ativos.
* Publicar ativos.
* Editar, mover e copiar ativos.
* Pesquisar, filtrar e pesquisar (inclui pesquisa de semelhança) ativos.
* Adicione valores e edite os valores nos campos de metadados, exceto no campo Tags inteligentes , que estão disponíveis no [!UICONTROL Básico] da guia de um ativo [!UICONTROL Propriedades] por padrão.
* Adicione e exclua representações estáticas.
* Baixe pastas, ativos e representações de ativos.
* Criar versões de ativos.
* Crie e execute tarefas de revisão em ativos.
* Anotar ativos.
* Adicionar ativos a [!DNL Sites] nas páginas do Localizador de conteúdo.
* Uso [!DNL Content Fragments].
* Usar REST HTTP e APIs GraphQL para [!DNL Content Fragments] e ativos de mídia referenciados, sob licença Sites.
* Integração do Marketing Cloud.
* Personalize e estenda a interface do usuário do gerenciamento de ativos.
* Acesse o Query Builder (API) para estender a funcionalidade de pesquisa.
* Crie tags estáticas.
* Crie projetos e tarefas.
* Fluxo de atividade (linha do tempo).
* Comentários e anotações.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Muitos casos de uso avançados de DAM são cumpridos por [!DNL Experience Manager Assets]. A licença da Media Library permite atender somente aos casos de uso listados usando o Media Library. Se um caso de uso não estiver listado, não o use com a licença do Media Library. Se tiver dúvidas, entre em contato com o Suporte ao cliente do Adobe.

Observe que não é possível usar tags inteligentes, [!DNL Asset] link , [!DNL Asset] seletor, marcação em massa, modificar workflows de ativos ou padrão [!DNL Adobe Experience Manager] interface do usuário para acessar o Media Library sem [!DNL Assets] licença.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Recursos do DAM em [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Descrição do produto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 descrição do produto no local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)


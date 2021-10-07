---
title: Usar o Media Library para o gerenciamento básico de ativos digitais
description: '[!DNL Experience Manager Assets] e Media Library para gerenciamento de ativos.'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
source-git-commit: 5462eb18c55a509712dab8fdbb653eb2d1889763
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Usar o Media Library para gerenciamento básico de ativos {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] A plataforma fornece diferentes recursos para gerenciar ativos. O Media Library permite que os usuários façam upload de um pequeno número de ativos para o repositório, pesquisem e usem nas páginas da Web e realizem tarefas simples de gerenciamento de ativos nos ativos.

O Media Library é uma solução leve de Gerenciamento de ativos digitais (DAM) que vem complementar com a licença [!DNL Adobe Experience Manager Sites]. [!DNL Sites] O é uma oferta do Web Content Management (WCM). O Media Library funciona com todos os recursos do Experience Manager.

[!DNL Adobe Experience Manager Assets] está disponível separadamente para compra. [!DNL Experience Manager Assets] O permite o gerenciamento robusto de ativos por meio de casos de uso corporativos, personalizações de metadados, esquemas, pesquisa e interface do usuário, além do que a Media Library oferece.

## Requisitos de licenciamento {#avail-media-library-license}

Os clientes que têm [!DNL Sites] licença têm direito a usar o Media Library. Funciona com todos os componentes de [!DNL Experience Manager].

O Media Library é instalado como parte do Sites. Nenhuma licença ou pacote adicional é necessário além da licença e instalação do Sites.

## [!DNL Assets] versus Media Library {#assets-and-media-library}

O Experience Manager Assets fornece funcionalidade de DAM de nível empresarial. A funcionalidade de ativos é fornecida com [!DNL Experience Manager] em um único pacote. No entanto, os usuários que não compraram uma licença do Assets não têm direito a usar os recursos avançados do DAM. Sem a licença do Assets, somente [os recursos do Media Library](#use-media-library) estão disponíveis.

Se quiser impedir o uso não intencional de [!DNL Assets] recursos que você não licenciou, remova todos os workflows, componentes, taxonomias, opções e o administrador [!DNL Assets] específicos [!DNL Experience Manager]. [!DNL Assets] Isso impede que seus usuários utilizem acidentalmente recursos [!DNL Assets] que você não licenciou.

## Usar o Media Library {#use-media-library}

A Media Library abrange os seguintes casos de uso:

* Forneça recursos básicos do DAM para páginas da Web criadas usando [!DNL Adobe Experience Manager Sites].
* Formulários adaptáveis e comunicações criadas usando [!DNL Adobe Experience Manager Forms].
* Experiências de tela digital criadas usando [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] REST APIs HTTP para operações sem periféricos.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Basic metadata properties
* Tag management
* Version control
* Static renditions
* Projects, tasks, workflow authoring
* Activity stream (timeline)
* Query Builder (API)
* Marketing Cloud integration
* User interface customization and extension
* Comments and annotation
-->

Para usar a funcionalidade Media Library, você pode usar a interface do usuário padrão [!DNL Experience Manager]. O Media Library faz parte da instalação [!DNL Experience Manager Sites] e nenhuma interface ou complemento separado é necessário. Usando a interface existente, os usuários do Media Library têm direito a realizar as seguintes tarefas:

* Crie pastas para organizar ativos.
* Fazer upload de ativos.
* Publicar ativos.
* Editar, mover e copiar ativos.
* Pesquisar, filtrar e pesquisar (inclui pesquisa de semelhança) ativos.
* Adicione valores e edite os valores nos campos de metadados, exceto no campo Tags inteligentes , que estão disponíveis na guia [!UICONTROL Básico] da página [!UICONTROL Propriedades] de um ativo por padrão.
* Adicione e exclua representações estáticas.
* Baixe pastas, ativos e representações de ativos.
* Criar versões de ativos.
* Crie e execute tarefas de revisão em ativos.
* Anotar ativos.
* Adicione ativos a [!DNL Sites] páginas por meio do Localizador de conteúdo.
* Uso [!DNL Content Fragments].
* Use HTTP REST e APIs GraphQL para [!DNL Content Fragments] e ativos de mídia referenciados, sob licença Sites.
* Integração do Marketing Cloud.
* Personalize e estenda a interface do usuário do gerenciamento de ativos.
* Acesse o Query Builder (API) para estender a funcionalidade de pesquisa.
* Crie tags estáticas.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Muitos casos de uso avançados do DAM são cumpridos por [!DNL Experience Manager Assets]. A licença da Media Library permite atender somente aos casos de uso listados usando o Media Library. Se um caso de uso não estiver listado, não o use com a licença do Media Library. Se tiver dúvidas, entre em contato com o Suporte ao cliente do Adobe.

Observe que não é possível usar tags inteligentes, link [!DNL Asset], seletor [!DNL Asset], marcação em massa, modificação de workflows de ativos sem licença [!DNL Assets].

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Recursos do DAM em [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Descrição do produto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 descrição do produto no local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)


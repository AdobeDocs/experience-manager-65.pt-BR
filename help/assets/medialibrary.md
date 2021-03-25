---
title: Use a Biblioteca de mídia para o gerenciamento básico de ativos digitais
description: '[!DNL Experience Manager Assets] e Biblioteca de mídia para gerenciamento de ativos.'
contentOwner: AG
role: Arquiteto, Líder
translation-type: tm+mt
source-git-commit: 15c525746a613eb33cd09b7ff476f43aa18b146b
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---


<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Use a Biblioteca de mídia para o gerenciamento básico de ativos {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] A plataforma fornece diferentes recursos para gerenciar ativos. A Biblioteca de mídia permite que os usuários façam upload de um pequeno número de ativos no repositório, pesquisem e usem nas páginas da Web e realizem tarefas simples de gerenciamento de ativos nos ativos.

A Biblioteca de mídia é uma solução leve de Gerenciamento de ativos digitais (DAM) que vem complementar com a licença [!DNL Adobe Experience Manager Sites]. [!DNL Sites] O é uma oferta do Web Content Management (WCM). A Biblioteca de mídia funciona com todos os recursos do Experience Manager.

[!DNL Adobe Experience Manager Assets] está disponível separadamente para compra. [!DNL Experience Manager Assets] O permite o gerenciamento robusto de ativos por meio de casos de uso corporativos, personalizações de metadados, esquemas, pesquisa e interface do usuário, além do que a Biblioteca de mídia oferece.

## Requisitos de licenciamento {#avail-media-library-license}

Os clientes que têm [!DNL Sites] licença têm direito a usar a Biblioteca de mídia. Funciona com todos os componentes de [!DNL Experience Manager].

A Biblioteca de mídia é instalada como parte do Sites. Nenhuma licença ou pacote adicional é necessário além da licença e instalação do Sites.

## [!DNL Assets] versus Biblioteca de mídia  {#assets-and-media-library}

O Experience Manager Assets fornece funcionalidade de DAM de nível corporativo. A funcionalidade de ativos é fornecida com [!DNL Experience Manager] em um único pacote. No entanto, os usuários que não compraram uma licença do Assets não têm direito a usar os recursos avançados do DAM. Sem a licença do Assets, somente os [recursos da Biblioteca de mídia](#use-media-library) estão disponíveis.

Se quiser impedir o uso não intencional de [!DNL Assets] recursos que você não licenciou, remova todos os workflows, componentes, taxonomias, opções e o administrador [!DNL Assets] específicos [!DNL Experience Manager]. [!DNL Assets] Isso impede que seus usuários utilizem acidentalmente recursos [!DNL Assets] que você não licenciou.

## Usar biblioteca de mídia {#use-media-library}

A Biblioteca de mídia abrange os seguintes casos de uso:

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

Para usar a funcionalidade Biblioteca de mídia, você pode usar a interface de usuário padrão [!DNL Experience Manager]. A Biblioteca de mídia faz parte da instalação [!DNL Experience Manager Sites] e nenhuma interface ou complemento separado é necessário. Usando a interface existente, os usuários da Biblioteca de mídia têm direito a realizar as seguintes tarefas:

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

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>Muitos casos de uso avançados do DAM são cumpridos por [!DNL Experience Manager Assets]. A licença da Biblioteca de mídia permite atender somente aos casos de uso listados usando a Biblioteca de mídia. Se um caso de uso não estiver listado, não o use com a licença Biblioteca de mídia. Caso tenha dúvidas, entre em contato com o Atendimento ao cliente do Adobe.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Recursos do DAM em [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Descrição do produto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 descrição do produto no local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)


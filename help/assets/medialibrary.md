---
title: Use a Biblioteca de mídia para o gerenciamento básico de ativos digitais
description: '[!DNL Experience Manager Assets] e Biblioteca de mídia para gerenciamento de ativos.'
contentOwner: AG
role: Developer, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---


# Usar a Biblioteca de mídia para o gerenciamento básico de ativos {#manage-assets-using-media-library}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

A plataforma [!DNL Adobe Experience Manager] fornece diferentes recursos para gerenciar ativos. A Media Library permite que os usuários façam upload de um pequeno número de ativos no repositório, pesquisem e usem esses ativos nas páginas da Web e realizem tarefas simples de gerenciamento de ativos nos ativos.

A Media Library é uma solução leve de gerenciamento de ativos digitais (DAM) que vem complementar com a licença do [!DNL Adobe Experience Manager Sites]. [!DNL Sites] é uma oferta de WCM (Web Content Management, gerenciamento de conteúdo da Web). A Biblioteca de mídia funciona com todos os recursos do Experience Manager.

A licença do [!DNL Adobe Experience Manager Assets] está disponível separadamente para compra. O [!DNL Experience Manager Assets] permite uma manipulação robusta de ativos por meio de casos de uso de empresa, personalizações de metadados, esquemas, pesquisa e interface de usuário, além de muitos outros recursos além do que a Biblioteca de Mídia oferece.

## Requisitos de licenciamento {#avail-media-library-license}

Os clientes que possuem licença do [!DNL Sites] estão autorizados a usar a Biblioteca de Mídia. Funciona com todos os componentes de [!DNL Experience Manager].

A Biblioteca de mídia é instalada como parte do Sites. Não é necessária nenhuma licença ou pacote adicional além da licença e instalação do Sites.

## [!DNL Assets] versus Biblioteca de mídia {#assets-and-media-library}

A Experience Manager Assets oferece a funcionalidade DAM de nível empresarial. A funcionalidade do Assets é fornecida com [!DNL Experience Manager] em um único pacote. No entanto, os usuários que não compraram uma licença do Assets não estão autorizados a usar os recursos avançados do DAM. Sem a licença do Assets, somente os [recursos da Biblioteca de mídia](#use-media-library) estão disponíveis.

Se você quiser impedir o uso não intencional dos recursos do [!DNL Assets] que não são licenciados, remova todos os fluxos de trabalho, componentes, taxonomias, opções e o administrador do [!DNL Assets] específicos do [!DNL Assets] do [!DNL Experience Manager]. Isso impede que seus usuários usem acidentalmente os recursos do [!DNL Assets] que você não licenciou.

## Usar biblioteca de mídia {#use-media-library}

A Media Library fornece recursos básicos do DAM para os seguintes casos de uso:

* Páginas da Web criadas usando [!DNL Adobe Experience Manager Sites].
* Formulários adaptáveis e comunicações criadas usando o [!DNL Adobe Experience Manager Forms].
* Experiências de tela digital criadas com o [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] APIs REST HTTP para operações headless.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Para usar a funcionalidade Biblioteca de Mídia, você pode usar a interface de usuário padrão [!DNL Experience Manager]. A Biblioteca de Mídia faz parte da instalação do [!DNL Experience Manager Sites] e nenhuma interface ou complemento separado é necessário. Usando a interface existente, os usuários da Biblioteca de mídia estão autorizados a realizar as seguintes tarefas:

* Criar pastas para organizar ativos.
* Fazer upload de ativos.
* Publicar ativos.
* Editar, mover e copiar ativos.
* Procurar, filtrar e pesquisar (inclui pesquisa de semelhança) ativos.
* Adicione valores e edite-os nos campos de metadados, exceto no campo Tags inteligentes, que estão disponíveis por padrão na guia [!UICONTROL Básico] da página [!UICONTROL Propriedades] de um ativo.
* Adicionar e excluir representações estáticas.
* Baixe pastas, ativos e representações de ativos.
* Criar versões de ativos.
* Criar e executar tarefas de revisão em ativos.
* Anotar ativos.
* Adicionar ativos a [!DNL Sites] páginas por meio do Localizador de conteúdo.
* Usar [!DNL Content Fragments].
* Use APIs HTTP REST e GraphQL para [!DNL Content Fragments] e ativos de mídia referenciados, sob a licença do Sites.
* Integração com o Marketing Cloud.
* Personalizar e estender a interface do usuário do gerenciamento de ativos.
* Acesse o Construtor de consultas (API) para estender a funcionalidade de pesquisa.
* Criar tags estáticas.
* Crie projetos e tarefas.
* Fluxo de atividade (linha do tempo).
* Comentários e anotações.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Muitos casos de uso de DAM avançados são preenchidos por [!DNL Experience Manager Assets]. A licença da Media Library permite preencher apenas os casos de uso listados usando a Media Library. Se um caso de uso não estiver listado, não o use com a licença da Biblioteca de mídia. Em caso de dúvidas, entre em contato com o Suporte ao cliente da Adobe.

Observe que você não pode usar marcas inteligentes, link [!DNL Asset], seletor [!DNL Asset], marcação em massa, modificar fluxos de trabalho de ativos ou a interface de usuário padrão [!DNL Adobe Experience Manager] para acessar a Biblioteca de Mídia sem a licença [!DNL Assets].

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [recursos DAM em [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html?lang=pt-BR)
>* [[!DNL Experience Manager] 6.5 Descrição do produto Managed Services](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 descrição do produto no local](https://helpx.adobe.com/br/legal/product-descriptions/adobe-experience-manager-on-premise.html)

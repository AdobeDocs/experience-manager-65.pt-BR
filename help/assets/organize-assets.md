---
title: Organize seus ativos digitais
description: Organize seus ativos digitais, imagens, arquivos, pastas e assim por diante usando o Experience Manager.
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
hide: true
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Organize seus ativos digitais {#organize-digital-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| Adobe Experience Manager (AEM) as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | Este artigo |

Todos os ativos digitais, metadados e conteúdo dos documentos do Microsoft® Office e PDF são extraídos e tornados pesquisáveis. A pesquisa permite uma filtragem sofisticada de ativos e respeita totalmente as permissões apropriadas. Os metadados são abordados em detalhes nos metadados no Digital Asset Management.

[!DNL Experience Manager Assets] O oferece suporte a várias maneiras de organizar o conteúdo. Você pode organizá-los de maneira hierárquica usando pastas ou de maneira não ordenada e ad hoc, usando, por exemplo, tags. Os usuários podem editar tags no Editor de ativos DAM, onde subativos, representações e metadados são exibidos.

## Organizar ativos em pastas {#organize-using-folders}

A maneira mais básica de organizar ativos é salvá-los em pastas. É análogo a organizar arquivos em pastas em seu sistema de arquivos local. Para obter mais informações sobre como criar e gerenciar pastas, consulte [Gerenciar ativos](manage-assets.md). A maneira como você nomeia arquivos e pastas, como organiza subpastas e como lida com os arquivos dentro dessas pastas pode ter um impacto significativo na maneira como esses ativos são processados. Usando estratégias consistentes e apropriadas de nomenclatura de arquivos e pastas, juntamente com boas práticas de metadados, você pode aproveitar ao máximo seu repositório de ativos digitais.

* Normalmente, o repositório de ativos digitais está sempre crescendo. Portanto, é importante formalizar o uso de metadados, a estrutura de pastas e a nomenclatura de arquivos no início do ciclo de criação de conteúdo.
* Use pastas somente para impor uma estrutura de armazenamento consistente para seus ativos digitais. Essa consistência ajuda a processar e gerenciar melhor seus ativos. Por exemplo, os ativos colocados nos seguintes tipos de pastas podem ajudar você a usar os [perfis a serem usados para processamento de ativos](processing-profiles.md):

   * **Pastas de desenvolvimento**: contém ativos digitais nos quais você está trabalhando atualmente.
   * **Pastas do cliente**: contém ativos digitais com base em clientes ou nomes de projeto.
   * **Pastas primárias**: contém ativos digitais originais.
   * **Pastas de representação**: contém representações e cópias dos ativos digitais originais e de origem.
   * **Pastas de tamanho de arquivo**: contém ativos digitais com base no tamanho de arquivos pequeno, médio ou grande.
   * **Pastas de preparo**: contém ativos digitais prontos para publicar ao vivo no site.
   * **Pastas do tipo MIME**: contém ativos digitais específicos para tipos MIME, como imagens, documentos e multimídia.
   * **Arquivar pastas**: contém ativos digitais desativados.
   * **Pastas baseadas em data**: contém ativos digitais com base em uma data de criação ou uma data da última modificação.

* Crie um diretório de pastas que provavelmente não serão alteradas para que qualquer personalização ou automação continue a funcionar. Por exemplo, os perfis de processamento atribuídos continuam a funcionar.
* Se um ativo já estiver publicado, você poderá usar [!DNL Experience Manager] para mover o ativo para outra pasta e republicar de seu novo local, o local do ativo original publicado ainda está disponível, juntamente com o ativo recém-republicado. No entanto, o ativo publicado original é *perdido* para [!DNL Experience Manager] e não podem ter a publicação desfeita. Portanto, como prática recomendada, primeiro cancele a publicação de um ativo e, em seguida, mova-o para uma pasta diferente.

## Organizar ativos usando tags {#use-tags-to-organize-assets}

Usando tags como metadados, você pode pesquisar ativos facilmente, criar coleções usando os resultados da pesquisa, aumentar a classificação de pesquisa para alguns ativos e usar algoritmos de inteligência artificial do Adobe Sensei para a descoberta de ativos.

[!DNL Adobe Experience Manager Assets] O usa um algoritmo de autoaprendizado para criar tags altamente descritivas que permitem encontrar o ativo correto com apenas alguns cliques. A marcação inteligente usa o Adobe Sensei, a inteligência artificial de Adobe e a estrutura de aprendizado de máquina, que podem ser treinadas para reconhecer e aplicar tags padrão e específicas de negócios a imagens. As Tags inteligentes também podem identificar conteúdo, palavras individuais ou frases e aplicar automaticamente tags descritivas aos ativos

Para obter mais informações, consulte os seguintes artigos:

* [Sobre tags no Experience Manager](/help/sites-authoring/tags.md)
* [Editar metadados de ativos](metadata.md)
* [Tags inteligentes aprimoradas no Assets](enhanced-smart-tags.md)

## Organizar como coleções {#organize-as-collections}

Com coleções de ativos em [!DNL Experience Manager Assets], você pode simplificar a capacidade de criar, editar e compartilhar ativos entre usuários. Crie vários tipos de coleções com base na maneira como você as usa, incluindo coleções que contêm uma lista de referência estática de ativos, pastas e coleções e coleções que extraem ativos com base em critérios de pesquisa. Você também pode criar coleções com ativos de diferentes locais e compartilhá-las com vários usuários com diferentes níveis de privilégios de acesso, visualização e edição.

Para obter mais informações, consulte [gerenciar coleções](manage-collections.md).

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organize seus ativos para usar perfis {#organize-to-use-profiles}

Um perfil de processamento contém [!DNL Assets] processar comandos que se aplicam a ativos que são carregados em pastas predefinidas. Os perfis são usados para automatizar o processamento de conteúdo de uma pasta ou de ativos carregados recentemente. Você pode usar perfis para organizar melhor seus ativos.

A padronização do uso de metadados, da nomeação de arquivos e da estrutura de pastas garante que, à medida que seu pool de ativos digitais cresce, você possa aplicar perfis de processamento a pastas com mais precisão e consistência.

>[!MORELIKETHIS]
>
>* [Perfis para processar metadados, imagens e vídeos](processing-profiles.md).
>* [Perfis de metadados](/help/assets/metadata-config.md#metadata-profiles).
>* [Perfis de vídeo](video-profiles.md).
>* [Perfis de imagem do Dynamic Media](image-profiles.md).

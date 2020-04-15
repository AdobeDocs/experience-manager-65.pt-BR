---
title: Organize seus ativos digitais
description: Organize seus ativos digitais, imagens, arquivos, pastas e assim por diante usando o Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Organize seus ativos digitais {#organize-digital-assets}

Todos os ativos digitais, metadados e conteúdo de documentos do Microsoft Office e PDF são extraídos e tornados pesquisáveis. A pesquisa permite a filtragem sofisticada de ativos e respeita totalmente as permissões adequadas. Os metadados são abordados detalhadamente em metadados no Gerenciamento de ativos digitais.

O AEM Assets oferece suporte a várias formas de organização de conteúdo. Você pode organizá-las de maneira hierárquica usando pastas ou pode organizá-las de forma não ordenada e ad-hoc, usando, por exemplo, tags. Os usuários podem editar tags no DAM Asset Editor, onde subativos, representações e metadados são exibidos.

## Organizar ativos em pastas {#organize-using-folders}

A maneira mais básica de organizar ativos é salvá-los em pastas. É análogo à organização de arquivos em pastas no nosso sistema de arquivos local. Para obter mais informações sobre como criar e gerenciar pastas, consulte [Gerenciar ativos](managing-assets-touch-ui.md). A forma como você nomeia arquivos e pastas, como você organiza as subpastas e como manipula os arquivos dessas pastas pode ter um impacto significativo na forma como esses ativos são processados. Usando estratégias de nomenclatura de arquivos e pastas consistentes e apropriadas, juntamente com boas práticas de metadados, você pode aproveitar ao máximo seu repositório de ativos digitais.

* Na maioria dos casos, seu repositório de ativos digitais está sempre crescendo. Portanto, é importante formalizar o uso de metadados, a estrutura de pastas e a nomeação de arquivos no início do ciclo de criação de conteúdo.
* Use pastas somente para impor uma estrutura de armazenamento consistente para seus ativos digitais. Essa consistência ajuda a processar e gerenciar melhor seus ativos. Por exemplo, os ativos colocados nos seguintes tipos de pastas podem ajudá-lo a usar os [perfis apropriados para o processamento](processing-profiles.md)de ativos:

   * **Pastas** de desenvolvimento: contém ativos digitais em que você está trabalhando no momento.
   * **Pastas** do cliente: contém ativos digitais com base em clientes ou nomes de projetos.
   * **Pastas** principais: contém ativos digitais originais de origem.
   * **Pastas** de representação: contém renderizações e cópias dos ativos digitais originais de origem.
   * **Pastas** de tamanho de arquivo: contém ativos digitais baseados em arquivos de tamanho pequeno, médio ou grande.
   * **Pastas** de preparo: contém ativos digitais que estão prontos para publicação ao vivo em seu site.
   * **Pastas** do tipo MIME: contém ativos digitais específicos para tipos MIME, como imagens, documentos e multimídia.
   * **Arquivar pastas**: contém ativos digitais desativados.
   * **Pastas** baseadas em data: contém ativos digitais com base em uma data de criação ou em uma data de última modificação.

* Crie um diretório de pastas que provavelmente não serão alteradas para que qualquer personalização ou automação continue funcionando. Por exemplo, os perfis de processamento atribuídos continuam funcionando.
* Se um ativo já tiver sido publicado, você usará o AEM para mover o ativo para outra pasta e republicar de seu novo local, o local original do ativo publicado ainda estará disponível, juntamente com o ativo recém-publicado. O ativo publicado original, no entanto, é *perdido* para o AEM e não pode ser despublicado. Portanto, como prática recomendada, primeiro cancele a publicação de um ativo e depois mova-o para uma pasta diferente.

## Organizar ativos usando tags {#use-tags-to-organize-assets}

Usando tags, como metadados, você pode pesquisar facilmente ativos, criar coleções usando os resultados da pesquisa, aumentar a classificação de pesquisa para alguns ativos e aproveitar os algoritmos AI do Adobe Sensei para a descoberta de ativos.

Os ativos Adobe Experience Manager usam um algoritmo de autoaprendizado para criar tags altamente descritivas que permitem encontrar o ativo certo em apenas alguns cliques. A marcação inteligente usa o Adobe Sensei, nossa inteligência artificial e estrutura de aprendizado de máquina, que pode ser treinada para reconhecer e aplicar tags padrão e específicas de negócios à imagem. Tags inteligentes também podem identificar conteúdo, palavras individuais ou frases e aplicar automaticamente tags descritivas a ativos

Para obter mais informações, consulte os seguintes artigos:

* [Sobre tags no AEM](/help/sites-authoring/tags.md)
* [Editar metadados de ativos](meta-edit.md)
* [Tags inteligentes aprimoradas em ativos](enhanced-smart-tags.md)

## Organizar como coleções {#organize-as-collections}

Com as coleções de ativos nos ativos do Experience Manager, você pode simplificar a capacidade de criar, editar e compartilhar ativos entre usuários. Crie vários tipos de coleções com base na maneira como você as usa, incluindo coleções que contêm uma lista de referência estática de ativos, pastas e coleções, bem como coleções que extraiam ativos com base em critérios de pesquisa.  Você também pode criar coleções com ativos de diferentes locais e compartilhá-las com vários usuários com diferentes níveis de privilégios de acesso, visualização e edição.

Para obter mais informações, consulte [gerenciar coleções](managing-collections-touch-ui.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organize seus ativos para usar perfis {#organize-to-use-profiles}

Um perfil de processamento contém comandos de processamento do Assets que se aplicam a ativos que são carregados em pastas predefinidas. Os Perfis são usados para automatizar o processamento do conteúdo de uma pasta ou dos ativos carregados recentemente. Você pode aproveitar perfis para organizar melhor seus ativos.

A padronização do uso de metadados, da nomeação de arquivos e da estrutura de pastas garante que, à medida que o pool de ativos digitais cresce, você aplique perfis de processamento a pastas com maior precisão e consistência.

Para obter mais informações sobre vários perfis que você pode criar e gerenciar para processar ativos, consulte,

* [Perfis para processar metadados, imagens e vídeos](processing-profiles.md)
* [Perfis de metadados](metadata-profiles.md)
* [perfis de vídeo](video-profiles.md)
* [perfis de imagem do Dynamic Media](image-profiles.md)

---
title: Práticas recomendadas de integração do AEM e da Creative Cloud
description: Práticas recomendadas para integrar o AEM com a Adobe Creative Cloud a fim de simplificar os fluxos de trabalho de transferência de ativos e obter o máximo de eficiência.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Práticas recomendadas de integração do AEM e da Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.4 article that's behind this article in terms of content streamlining and structuring.
-->

O Adobe Experience Manager Assets é uma solução de gerenciamento de ativos digitais (DAM) que pode se integrar à Adobe Creative Cloud para ajudar os usuários do DAM a trabalharem em conjunto com as equipes de criação, simplificando a colaboração no processo de criação de conteúdo.

A Adobe Creative Cloud fornece às equipes criativas um ecossistema de soluções e serviços para ajudá-las a criar ativos digitais. Inclui aplicativos para desktop e dispositivos móveis, serviços em nuvem como armazenamento com sincronização de desktop ou experiência na Web, bem como mercados como o Adobe Stock.

Leia para saber quais integrações escolher entre o desktop e o DAM de nível corporativo com base no caso de uso e quais são as práticas recomendadas associadas para os fluxos de trabalho de conexão.

>[!NOTE]
>
>O compartilhamento de pastas do AEM para a Creative Cloud está obsoleto e não é mais abordado neste guia. A Adobe recomenda usar recursos mais recentes, como o [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) ou o aplicativo [de desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) AEM, para fornecer ao usuário criativo acesso aos ativos gerenciados no AEM.

## Necessidades de colaboração de criativos, profissionais de marketing e usuários de DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superfícies envolvidas |
|---|---|---|
| Simplifique a experiência para criativos em desktop | Simplifique o acesso a ativos de um DAM (AEM Assets) para profissionais criativos, ou, mais amplamente, para usuários de desktop que trabalham em aplicativos nativos de criação de ativos. Eles precisam de uma maneira fácil e direta de descobrir, usar (abrir), editar e salvar alterações no AEM, bem como fazer upload de novos arquivos. | Ambiente de trabalho Win ou Mac; Aplicativos da Creative Cloud |
| Fornecer ativos prontos para uso de alta qualidade do Adobe Stock | Os profissionais de marketing ajudam a acelerar o processo de criação de conteúdo auxiliando na seleção de fontes e na descoberta de ativos. Profissionais criativos usam os ativos aprovados diretamente de suas ferramentas criativas. | AEM Assets; Mercado do Adobe Stock; campos de metadados |
| Distribuir e compartilhar ativos por organizações | Os departamentos internos/locais e parceiros externos, distribuidores e agências usam os ativos aprovados compartilhados pela organização-mãe. A organização deseja compartilhar com segurança e facilidade os ativos criados para uma reutilização mais ampla. | Portal de marcas, Compartilhamento de ativos comuns |

## Ofertas da Adobe para dar suporte à necessidade de colaboração {#adobe-offerings-to-support-the-collaboration-need}

| Proposta de valor para as pessoas envolvidas | Oferta da Adobe | Superfícies envolvidas |
|---|---|---|
| Os usuários criativos descobrem ativos do AEM, os abrem e usam, editam e carregam alterações no AEM, bem como carregam novos arquivos no AEM, sem sair dos aplicativos da Creative Cloud. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator e InDesign |
| Os usuários empresariais simplificam a abertura e o uso de ativos, a edição e o upload de alterações no AEM e o upload de novos arquivos no AEM a partir do ambiente de desktop. Eles usam uma integração genérica para abrir qualquer tipo de ativo no aplicativo de desktop nativo, incluindo os que não são da Adobe. | [Aplicativo de desktop do AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | Aplicativo de desktop AEM no desktop Win e Mac |
| Os profissionais de marketing e usuários comerciais descobrem, visualizam, licenciam e salvam e gerenciam os ativos do Adobe Stock no AEM. Os ativos licenciados e salvos fornecem metadados selecionados do Adobe Stock para melhor controle. | [Integração do Experience Manager e do Adobe Stock](aem-assets-adobe-stock.md) | Interface da Web AEM |

Este artigo foca principalmente os dois primeiros aspectos das necessidades de colaboração. A distribuição e a aquisição de ativos em escala são brevemente mencionadas como um caso de uso. Para essas necessidades, considere o Adobe Brand Portal ou o Asset Share Commons. Soluções alternativas, como o Portal [de](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html)marca, que podem ser criadas com base nos componentes do [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) , o [Link Share](/help/assets/link-sharing.md)usando os Ativos [do](/help/assets/managing-assets-touch-ui.md) Experience Manager devem ser revisadas com base em requisitos específicos.

![Conexões da Creative Cloud para o AEM: Decidir qual capacidade usar](assets/creative-connections-aem.png)

### Mapeamento de casos de uso e soluções da Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso de uso | Adobe Asset Link | Aplicativo de desktop do AEM | Observações / Outras soluções |
|---|---|---|---|
| Discover - procurar pastas do AEM | Sim | AEM Web UI + ações da área de trabalho | Ao navegar pelo compartilhamento de rede, desative as miniaturas para evitar o download de arquivos binários de ativos. |
| Discover - acessar coleções do AEM | Sim | AEM Web UI + ações da área de trabalho |  |
| Discover - pesquisar ativos do AEM | Sim | AEM Web UI + ações da área de trabalho |  |
| Usar - ativo aberto | Sim | Sim - para qualquer aplicativo | [Abrir da interface](managing-assets-touch-ui.md#previewing-assets) da Web ou do Finder |
| Usar - colocar o ativo do AEM em um documento | Sim - incorporação | Sim - vinculação ou incorporação | O aplicativo de desktop AEM dá acesso aos ativos como arquivos no sistema de arquivos local. Esses links nos aplicativos nativos são representados por caminhos locais. |
| Editar - abrir para edição | Sim - Ação de check-out | Sim - ação de abertura (no compartilhamento de rede) | [O check-out no AAL](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) salva o ativo na conta de armazenamento da Creative Cloud do usuário (sincronizada pelo aplicativo da Creative Cloud) por padrão. |
| Editar - trabalho em andamento fora do AEM | Sim - ativo disponível na conta de armazenamento da Creative Cloud do usuário sincronizada ao desktop. | Sim |  |
| Editar - carregar alterações | Sim - ação [de](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) check-in com comentário opcional | Sim |  |
| Carregar - único arquivo | Sim - carrega o documento ativo atual | Sim | [Fazer upload por meio da interface da Web](managing-assets-touch-ui.md#uploading-assets) |
| Carregar - vários arquivos / estruturas hierárquicas de pastas | Não | Sim | [Carregar por interface](managing-assets-touch-ui.md#uploading-assets)da Web;ferramenta ou script<br>personalizado |
| Misc - usuário e login | O usuário da Creative Cloud conectado ao aplicativo de desktop da Creative Cloud é reconhecido (SSO) | Usuário/logon do AEM | Os usuários de ambas as soluções contam com a cota de usuários do AEM. |
| Diversos - rede e acesso | Exige acesso da área de trabalho do usuário à implantação do AEM pela rede | Exige acesso da área de trabalho do usuário à implantação do AEM pela rede | O Adobe Asset Link não compartilha o ambiente proxy de rede. |
| Diversos - Migrar um grande número de ativos | Não | Não | [Guia de migração](assets-migration-guide.md) |

Para suportar casos de uso de distribuição de ativos, outras soluções devem ser consideradas:

* [Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) de marca para um complemento configurável de SaaS aos ativos AEM para publicar ativos.
* As soluções personalizadas são criadas com base na base de código [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) .
* Compartilhamento [de](/help/assets/link-sharing.md) link AEM para compartilhar ativos ad hoc usando links.
* [Interface](/help/assets/managing-assets-touch-ui.md) da Web do AEM Assets com áreas para terceiros protegidos pela configuração do Controle de acesso AEM e com ajustes necessários de configuração de TI/rede, dando a esses usuários externos acesso ao AEM.

## Conceitos-chave e casos de uso {#key-concepts-and-use-cases}

### Glossário de termos comuns {#glossary-of-common-terms}

* **** Trabalho em andamento ou trabalho em andamento criativo (WIP): Uma fase no ciclo de vida do ativo em que um ativo sofre várias alterações e normalmente ainda não está pronto para ser compartilhado com equipes mais amplas.
* **** Ativos prontos para criação: Os ativos que estão prontos para serem compartilhados com uma equipe mais ampla ou que foram selecionados/aprovados pela equipe criativa para compartilhamento com equipes de marketing ou LOB.
* **** Aprovações de ativos: O processo de aprovação que executa ativos já carregados no DAM, que normalmente inclui aprovações de marca, aprovações legais e assim por diante.
* **** Ativo final: Um ativo que passou por todas as aprovações/marcações de metadados e está pronto para ser usado pela equipe mais ampla. Esse ativo é armazenado no DAM e disponibilizado a todos os usuários (ou a todos os interessados). Ele pode ser usado em canais de marketing ou por equipes criativas para criar designs.
* **** Atualização/alteração de ativos secundários: Uma pequena e rápida mudança em um ativo digital. Geralmente é feito em resposta a uma solicitação de retoque ou edição secundária, revisão de ativos ou aprovação (por exemplo, reposição, alteração do tamanho do texto, ajuste da saturação/brilho, cor e assim por diante).
* **** Principais atualizações/alterações de ativos: Uma mudança em um ativo digital que requer trabalho considerável, e às vezes deve ser feita por um período mais longo. Normalmente, inclui várias alterações. O ativo deve ser salvo várias vezes durante a atualização. As principais atualizações de ativos normalmente fazem com que o ativo informe uma fase WIP.
* **** DAM: Gerenciamento de ativos digitais. Neste documento, ele é sinônimo de ativos AEM Experience Manager, a menos que especificamente mencionado o contrário.
* **** Usuário criativo: Um profissional criativo, que cria ativos digitais usando aplicativos e serviços da Creative Cloud. Em alguns casos, um usuário criativo pode ser membro de uma equipe criativa que pode usar a Creative Cloud, mas não cria ativos digitais (como um diretor criativo ou gerente de equipe criativa).
* **** Usuário do DAM: Um usuário típico de um sistema DAM. Dependendo da organização, um usuário do DAM pode ser um usuário de marketing ou não, por exemplo, um usuário de Linha de Negócios (LOB), um bibliotecário, um usuário de vendas e assim por diante.

### Considerações ao usar a integração do AEM e da Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

* Consulte Práticas recomendadas de aplicativos [para desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* Consulte Integração [do Adobe Stock](aem-assets-adobe-stock.md)
* Consulte Link de ativos [da Adobe](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Este é um breve resumo das práticas recomendadas para a integração do Experience Manager e da Creative Cloud. Leia o resto deste documento para obter a compreensão detalhada deles.

* **** Para usuários criativos, trabalhando no Photoshop, InDesign ou Illustrator: O Adobe Asset Link fornece a melhor experiência do usuário, incluindo a manipulação limpa do Work in progress em ativos com check-out do AEM
* **** Para simplificar o acesso a ativos do desktop para qualquer formato de arquivo ou aplicativo genérico: usar o aplicativo de desktop AEM
* **** Entenda por que e quando armazenar ativos no DAM: Atualizações a serem disponibilizadas para a equipe mais ampla em sua organização
* **** Considere o volume de ativos compartilhados: Se o caso de uso for a distribuição de ativos, a governança e a segurança podem ser os aspectos mais importantes. Considere o uso de ferramentas criadas para fazer isso em escala, como o Portal da Marca.
* **** Entenda o ciclo de vida do ativo: Saiba como os ativos são tratados em sua organização por equipes diferentes
* **** Lidar com salvamentos frequentes em ativos com cuidado: O Adobe Asset Link cuida disso para você com PS, AI, ID. Para outros aplicativos, não realize tarefas em andamento na pasta mapeada/compartilhada, a menos que você precise de todas as alterações no DAM

### Acesso aos ativos do Adobe Stock dos ativos AEM {#access-to-adobe-stock-assets-from-aem-assets}

[A integração](/help/assets/aem-assets-adobe-stock.md) do AEM e do Adobe Stock fornece aos usuários do AEM a capacidade de pesquisar, visualizar, licenciar e salvar ativos do Adobe Stock no AEM. Os ativos licenciados e salvos do Adobe Stock selecionaram metadados do Stock, que podem ser usados para pesquisá-los com filtros extras.

Alguns pontos importantes sobre essa integração:

* Quando os ativos do Adobe Stock são salvos no AEM, eles se tornam ativos AEM comuns, com o binário salvo no repositório do AEM. Alguns metadados relacionados ao Adobe Stock são salvos para o ativo no AEM, caso contrário, o processo de ingestão terá a mesma aparência de qualquer outro arquivo. Por exemplo, se as Tags inteligentes estiverem ativas, as tags serão adicionadas a esses ativos ao salvar.
* O ativo salvo no AEM é uma cópia, não um link de volta ao Adobe Stock.

**Trabalhar com ativos salvos do Adobe Stock no AEM na Creative Cloud**. Essa integração é independente do Adobe Asset Link, mas o Adobe Asset Link reconhece esses ativos salvos do Stock dessa forma e exibe metadados adicionais e ícones do Stock nesses ativos na interface de extensão do Adobe Asset Link no Photoshop, Illustrator ou InDesign. Os arquivos estão disponíveis para navegação, abertura e assim por diante - porque são ativos AEM comuns quando salvos no AEM.
Os usuários da Creative Cloud que trabalham em aplicativos da Creative Cloud com extensão do Adobe Asset Link presentes, além de terem acesso a ativos já licenciados do Adobe Stock ao AEM, também podem usar o painel Bibliotecas da Creative Cloud para pesquisar, visualizar e licenciar ativos do Adobe Stock.
Os ativos do Adobe Stock licenciados e salvos no AEM tornam-se disponíveis para equipes mais amplas que acessam a implantação dos ativos AEM, enquanto os ativos de licenciamento do Adobe Stock por meio do painel Bibliotecas da Creative Cloud os os tornam disponíveis somente para si mesmos por padrão em sua conta da Creative Cloud.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## Sobre o armazenamento de ativos em um DAM {#about-storing-assets-in-a-dam}

Para projetar um fluxo de trabalho eficiente entre equipes de criação e marketing/linha de negócios (LOB) e escolher os melhores recursos de suporte, é importante entender quando e por que os ativos são armazenados no DAM.

### Por que os ativos são armazenados no DAM {#why-assets-are-stored-in-dam}

Armazenar ativos no DAM os torna facilmente acessíveis e acessíveis. Ela garante que os ativos possam ser aproveitados por vários usuários em toda a organização ou ecossistema, o que inclui parceiros, clientes e assim por diante.

A maioria das organizações escolhe armazenar somente ativos relevantes para os processos de marketing/LOB de downstream (publicação em canais como canal da Web por meio do AEM Sites ou outros canais fornecidos pela Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e medidos pela Analytics Cloud, fornecendo a usuários/parceiros e assim por diante). Além disso, as organizações armazenam ativos que podem estar sujeitos a um processo de revisão/aprovação no DAM. Dessa forma, o DAM armazena principalmente ativos que têm grandes chances de serem aproveitados e evita armazenar ativos ociosos.

Armazenar ativos também está sujeito a considerações técnicas e de utilização de recursos. O DAM fornece serviços adicionais sobre ativos armazenados, incluindo extração de metadados, controle de versão, geração de visualizações/transcodificação, gerenciamento de referências e adição de informações de controle de acesso. Esses serviços consomem mais tempo e recursos de infraestrutura.

Geralmente, armazenar todos os ativos e atualizações não é desejável. Por exemplo, se as atualizações de ativos específicos forem de baixa qualidade e consumirem recursos excessivos, os ativos podem não ser armazenados no DAM.

#### Quando os ativos são armazenados no DAM {#when-assets-are-stored-in-dam}

Geralmente, as equipes criativas (e organizações) não estão interessadas em armazenar ativos em cada estágio do ciclo de vida do ativo. Por exemplo, eles evitam armazenar ativos nos seguintes casos:

* Ativos que ainda não foram finalizados ou estão sujeitos a experimentação
* Ativos que não passam no ciclo de análise da equipe interna/criativa
* Em comparação com o ativo em questão, a equipe tem melhores candidatos para representar seu trabalho para equipes externas

Normalmente, os seguintes ativos de classes são armazenados no DAM:

* Ativos que atingiram um determinado prazo de vencimento e são considerados prontos para serem partilhados
* Ativos pré-selecionados pela equipe criativa
* Formatos de ativos específicos que são utilizáveis ou solicitados pelo marketing, dependendo de um contrato ou contrato específico (por exemplo, arquivos JPG convertidos de arquivos RAW, TIFFs/imagens de originais PSD)

#### Quando as atualizações de ativos são armazenadas no DAM {#when-updates-to-assets-are-stored-in-dam}

Como regra, somente as atualizações de ativos relevantes para o conjunto mais amplo de usuários do DAM devem ser armazenadas no DAM. Ela garante que os usuários (marketing e funções semelhantes) visualizem somente as versões relevantes na linha do tempo do ativo DAM.

Normalmente, as alterações estão relacionadas aos principais marcos no ciclo de vida do ativo. Por exemplo, o ativo pronto para marketing ou uma atualização oficial com base na solicitação/revisão fornecida pela equipe criativa deve ser armazenado e controle de versão no DAM.

A atualização da equipe criativa para revisão pela equipe de marketing após uma solicitação de alteração no ativo existente no DAM é um exemplo de uma atualização relevante. Ele deve ser armazenado e controle de versão no DAM para referência adicional ou para reverter para a versão anterior.

A seguir estão exemplos de atualizações que normalmente não são relevantes:

* Versões antecipadas de ativos carregados antes de estarem prontos para a revisão de marketing
* Alterações criativas frequentes no ativo na fase de trabalho em andamento antes que as equipes de criação e marketing decidam que o ativo está pronto

### Acesso do usuário ao DAM {#user-access-to-dam}

O AEM Assets oferece suporte a dois tipos de usuários com base em seu acesso à implantação do AEM Assets. Normalmente, os usuários dentro da rede corporativa (firewall) têm acesso direto ao DAM. Outros usuários fora da rede corporativa não teriam acesso direto. O tipo de usuário determina quais integrações podem ser usadas do ponto de vista técnico.

#### Usuários criativos com acesso direto ao DAM {#creative-users-with-direct-access-to-dam}

Normalmente, equipes de criação interna ou agências/profissionais de criação integrados à rede interna têm acesso à instância do DAM, incluindo o logon do AEM. A infraestrutura de rede e AEM pode ser configurada para permitir o acesso direto a terceiros - normalmente organizações confiáveis, como agências que trabalham para um cliente - para ter acesso ao AEM pela rede (por exemplo, via VPN ou listagem de permissões de IP).

Nesses casos, o Adobe Asset Link ou o aplicativo de desktop AEM ajuda a fornecer acesso fácil aos ativos finais/aprovados e permite salvar ativos prontos para criação no DAM.

#### Usuários criativos sem acesso ao DAM {#creative-users-without-access-to-dam}

Agências externas e freelancers sem acesso direto à instância do DAM podem exigir acesso a ativos aprovados ou podem adicionar seus novos designs ao DAM.

Use as seguintes estratégias para fornecer acesso aos ativos finais/aprovados:

* Use o aplicativo desktop se o Link de ativo não funcionar.
* Usar o portal [de marcas do](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) AEM Assets para distribuir ativos com segurança para parceiros externos
* Usar uma implementação personalizada de um portal de distribuição e seleção de fornecedor com base no [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Use o controle de acesso configurado no AEM e a infraestrutura de rede necessária (por exemplo, a lista de permissões de VPN e IP) para dar a terceiros acesso a uma área de conteúdo dedicada no DAM. Eles podem usar a interface do usuário da Web do AEM para obter ativos e carregar novo conteúdo no DAM.

#### Trabalho em andamento em ativos do AEM {#work-in-progress-on-assets-from-aem}

Conforme discutido neste documento, é recomendável realizar atualizações importantes em ativos, às vezes chamados de trabalhos em andamento, sem que todas as edições sejam salvas no arquivo local e também carregadas no AEM como alterações. Isso acelera o trabalho de um usuário de desktop, limita a largura de banda da rede usada e mantém a linha do tempo dos ativos limpos e focados em atualizações importantes e controladas.

O Adobe Asset Link oferece um bom suporte para este caso de uso:

* Quando os usuários do Photoshop, InDesign ou Illustrator pretendem editar um arquivo, eles executam uma operação de Check-out no ativo fornecido
* O ativo é baixado em segundo plano, colocado na conta da Creative Cloud dos usuários sincronizada ao disco pelo aplicativo de desktop da Creative Cloud e o sinalizador de check-out é alternado no AEM no ativo para minimizar conflitos de edição
* A partir daí, o usuário trabalha em um arquivo armazenado localmente no local sincronizado e pode continuar trabalhando e salvando as alterações necessárias a qualquer frequência necessária
* Além disso, como o ativo está na conta da Creative Cloud, ele também está disponível em outros dispositivos que o usuário pode ter (por exemplo, pode ser aberto ou editado em um aplicativo dedicado da Creative Cloud para dispositivos móveis) e pode ser compartilhado com outros usuários da Creative Cloud para fins de colaboração.
* Quando o usuário criativo terminar com as alterações, ele poderá executar uma operação de Check-in no arquivo em seu aplicativo da Creative Cloud, com um comentário opcional. O ativo correspondente no AEM tem controle de versão e é atualizado com o novo binário. Usuários do AEM, como comerciantes ou LOB, têm acesso às principais alterações de ativos, ou marcos, por meio da interface do usuário da linha do tempo do ativo do AEM.

O aplicativo de desktop AEM fornece um compartilhamento de rede para ativos abertos no aplicativo nativo. Por padrão, todas as alterações feitas localmente são carregadas automaticamente no AEM depois de um breve período. Com tal configuração, salvas frequentes durante a fase de trabalho em andamento seriam carregadas para o AEM e controle de versão, criando muito tráfego de rede e possíveis desafios de escalabilidade - para não mencionar versões desnecessárias no AEM.

A abordagem recomendada aqui é usar uma opção no aplicativo de desktop do AEM para desativar atualizações automatizadas e fazer upload de alterações em ativos para o AEM manualmente, aproveitando a ação de upload de alterações na interface do usuário do Status do ativo do aplicativo.

#### Carregamento em massa para DAM {#bulk-upload-to-dam}

Você pode ter a necessidade de carregar simultaneamente um número maior de arquivos no DAM em alguns cenários, por exemplo:

* Carregar resultados de fotografias ou projetos maiores
* Fazer upload de ativos fornecidos por agências criativas
* Carregar ativos selecionados de um conjunto maior se a seleção for feita fora do DAM

A descrição refere-se ao upload de arquivos operacionalmente (por exemplo, toda semana ou com cada fotografia), como uma parte normal do fluxo de trabalho do usuário do desktop. As migrações de grandes ativos não são abordadas aqui.

Você pode aproveitar os seguintes recursos de upload:

* Para fazer upload de pastas grandes/hierárquicas em massa, use o aplicativo de desktop AEM que fornece funcionalidade de upload [de](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) pastas. Você também pode carregar estruturas hierárquicas de pastas. Os ativos são carregados em segundo plano e, portanto, não são vinculados a uma sessão do navegador da Web
* Para carregar alguns arquivos de uma única pasta, arraste os arquivos diretamente para a interface da Web ou use a opção Criar na interface da Web do AEM Assets.
* Dependendo dos requisitos de sua empresa, você também pode usar o carregador personalizado.

#### Gerenciar ativos digitais diretamente do desktop {#managing-digital-assets-directly-from-desktop}

Se você usar Compartilhamentos de arquivos de rede para gerenciar ativos digitais, o uso do compartilhamento de rede mapeado pelo aplicativo de desktop AEM pode ser visto como um substituto conveniente. Durante a transição dos compartilhamentos de arquivos de rede, a interface da Web do AEM fornece um conjunto avançado de recursos de Gerenciamento de ativos digitais que vão muito além do que é possível em um compartilhamento de rede (pesquisa, coleções, metadados, colaboração, visualizações e assim por diante), e o aplicativo de desktop do AEM fornece um link útil para conectar o repositório do DAM do lado do servidor ao trabalho no desktop.

Evite usar o aplicativo de desktop do AEM para gerenciar ativos diretamente no compartilhamento de rede dos ativos AEM. Por exemplo, evite usar o aplicativo de desktop do AEM para mover/copiar vários arquivos. Em vez disso, use a interface do usuário do AEM Assets para arrastar pastas do Finder/Explorer para o compartilhamento de rede ou use o recurso de Upload de pasta do AEM Assets.

#### Migração de ativos {#asset-migration}

Para planejar e executar migrações de ativos do sistema existente para um novo sistema ou migração de um grande volume de ativos armazenados em servidores, consulte o Guia [de](/help/assets/assets-migration-guide.md)Migração. As integrações de aplicativo de desktop AEM e AEM à Creative Cloud não oferecem suporte a essas migrações. Devido aos grandes volumes de ativos a serem ingeridos e aos requisitos adicionais em torno do mapeamento, transformação e ingestão de metadados, as migrações devem ser tratadas usando diferentes ferramentas e abordagens.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [Práticas recomendadas do aplicativo para desktop AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [AEM Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integração do AEM e do Adobe Stock](aem-assets-adobe-stock.md)


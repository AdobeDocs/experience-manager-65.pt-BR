---
title: Integração com as práticas recomendadas do Adobe Creative Cloud
description: Práticas recomendadas para integrar [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] a fim de simplificar os fluxos de trabalho de transferência de ativos e alcançar alta velocidade de conteúdo.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
translation-type: tm+mt
source-git-commit: c4cfb709162ca8f8f6e8508516c39542347c6bc4
workflow-type: tm+mt
source-wordcount: '3254'
ht-degree: 16%

---

# [!DNL Adobe Experience Manager] e práticas recomendadas  [!DNL Creative Cloud] de integração  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] O é uma solução de gerenciamento de ativos digitais (DAM) que pode ser integrada  [!DNL Adobe Creative Cloud] ao para ajudar usuários do DAM a trabalhar junto com equipes criativas, simplificando a colaboração no processo de criação de conteúdo.

[!DNL Adobe Creative Cloud] O fornece às equipes criativas um ecossistema de soluções e serviços para ajudá-las a criar ativos digitais. Ele inclui aplicativos móveis e de desktop, serviços em nuvem como armazenamento com sincronização de desktop ou experiência da Web, além de mercados como [!DNL Adobe Stock].

Leia para saber quais integrações devem ser escolhidas entre o desktop e o DAM de nível empresarial com base no seu caso de uso e quais são as práticas recomendadas associadas para os workflows de conexão.

>[!NOTE]
>
>[!DNL Experience Manager] o compartilhamento de  [!DNL Creative Cloud] pastas está obsoleto e não é mais abordado neste guia. O Adobe recomenda usar recursos mais recentes, como [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) ou [Experience Manager desktop app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html) para fornecer ao usuário criativo acesso a ativos gerenciados em [!DNL Experience Manager].

## Necessidades de colaboração de criadores, profissionais de marketing e usuários de DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superfícies envolvidas |
|---|---|---|
| Simplifique a experiência para criações no desktop | Simplifique o acesso a ativos a partir de um DAM ([!DNL Experience Manager Assets]) para profissionais criativos ou, de maneira mais ampla, para usuários em desktop que trabalham em aplicativos de criação de ativos nativos. Eles precisam de uma maneira fácil e direta de descobrir, usar (abrir), editar e salvar alterações em [!DNL Experience Manager], bem como fazer upload de novos arquivos. | Área de trabalho Win ou Mac; [!DNL Creative Cloud] aplicativos |
| Fornecer ativos prontos para uso e de alta qualidade de [!DNL Adobe Stock] | Os profissionais de marketing ajudam a acelerar o processo de criação de conteúdo, auxiliando no fornecimento e descoberta de ativos. Profissionais de criação usam os ativos aprovados diretamente de suas ferramentas criativas. | [!DNL Experience Manager Assets];  [!DNL Adobe Stock] Mercado; campos de metadados |
| Distribuir e compartilhar ativos por organizações | Os departamentos internos/ramificações locais e parceiros externos, distribuidores e agências usam os ativos aprovados compartilhados pela organização pai. A organização deseja compartilhar com segurança e facilidade os ativos criados para reutilização mais ampla. | Brand Portal, Compartilhamento de Ativos Commons |

## Ofertas do Adobe para dar suporte à necessidade de colaboração {#adobe-offerings-to-support-the-collaboration-need}

| Proposta de valor para as personas envolvidas | oferta de Adobe | Superfícies envolvidas |
|---|---|---|
| Os usuários criativos descobrem ativos de [!DNL Experience Manager], os abrem e usam, editam e carregam alterações em [!DNL Experience Manager], bem como carregam novos arquivos em [!DNL Experience Manager], sem sair de [!DNL Creative Cloud] aplicativos. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator], e  [!DNL Adobe InDesign]. |
| Os usuários empresariais simplificam a abertura e o uso de ativos, a edição e o upload de alterações para [!DNL Experience Manager] e o upload de novos arquivos para [!DNL Experience Manager] a partir do ambiente de trabalho. Eles usam uma integração genérica para abrir qualquer tipo de ativo no aplicativo de desktop nativo, incluindo os não-Adobe. | [Aplicativo de desktop do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] aplicativo de desktop no desktop Win e Mac |
| Os profissionais de marketing e usuários empresariais descobrem, visualizam, licenciam e salvam e gerenciam os ativos [!DNL Adobe Stock] de dentro de [!DNL Experience Manager]. Os ativos licenciados e salvos fornecem [!DNL Adobe Stock] metadados selecionados para melhor governança. | [Integração do Experience Manager e Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interface da Web |

Este artigo foca principalmente nos dois primeiros aspectos das necessidades de colaboração. A distribuição e o fornecimento de ativos em escala são brevemente mencionadas como um caso de uso. Para essas necessidades, considere o Adobe Brand Portal ou o Asset Share Commons. Soluções alternativas, como [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), soluções que podem ser criadas com base nos componentes [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Link Share](/help/assets/link-sharing.md), usando [Experience Manager Assets](/help/assets/manage-assets.md) devem ser revisadas com base em requisitos específicos.

![Conexões Creative Cloud para Experience Manager, decidir qual capacidade usar](assets/creative-connections-aem.png)

### Mapeamento de casos de uso e soluções Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso de uso  | [!DNL Adobe Asset Link] | Aplicativo de desktop do [!DNL Experience Manager]  | Observações / Outras soluções |
|---|---|---|---|
| Discover - procurar pastas do DAM | Sim | [!DNL Experience Manager] Interface da Web e ações da área de trabalho |  |
| Discover - acessar coleções de DAM | Sim | [!DNL Experience Manager] Interface da Web e ações da área de trabalho |  |
| Discover - pesquisar ativos do DAM | Sim | [!DNL Experience Manager] Interface da Web e ações da área de trabalho |  |
| Usar - abrir ativo | Sim | Sim | [Abrir do ](manage-assets.md#previewing-assets) interface da Web ou do Finder |
| Usar - colocar ativo do DAM em um documento | Sim - incorporação | Sim - vinculação ou incorporação | [!DNL Experience Manager] o aplicativo de desktop fornece acesso a ativos como arquivos no sistema de arquivos local. Esses links nos aplicativos nativos são representados por caminhos locais. |
| Editar - abrir para edição | Sim - Ação de check-out | Sim - Abrir ação (no compartilhamento de rede) | [O check-out no ](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) AAL salva o ativo na conta de armazenamento da creative cloud do usuário (sincronizada pelo aplicativo do Creative Cloud) por padrão. |
| Editar - trabalho em andamento fora do DAM | Sim - Ativo disponível na conta de armazenamento de Creative Cloud do usuário sincronizada com o desktop. | Sim |  |
| Editar - fazer upload de alterações | Sim - [Ação de check-in](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) com comentário opcional | Sim |  |
| Upload - arquivo único | Sim - carrega o documento ativo atual | Sim | [Fazer upload por meio da interface da Web](manage-assets.md#uploading-assets) |
| Upload - vários arquivos / estruturas hierárquicas de pastas | Não | Sim | [Faça upload via interface da Web ](manage-assets.md#uploading-assets) ou por meio de script ou ferramenta personalizada. |
| Misc - usuário e logon | O usuário Creative Cloud conectado ao aplicativo de desktop Creative Cloud é reconhecido (SSO) | [!DNL Experience Manager] usuário e credenciais | Os usuários de ambas as soluções contam para a cota de usuário [!DNL Experience Manager]. |
| Misc - rede e acesso | Requer acesso do desktop do usuário para [!DNL Experience Manager] implantação pela rede | Requer acesso do desktop do usuário para [!DNL Experience Manager] implantação pela rede | [!DNL Adobe Asset Link] não compartilha o ambiente proxy de rede. |
| Diversos - Migrar um grande número de ativos | Não | Não | [Guia de migração de ativos](assets-migration-guide.md) |

Para suportar casos de uso de distribuição de ativos, outras soluções devem ser consideradas:

* [Brand ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portalpara um complemento configurável SaaS  [!DNL Experience Manager Assets] para publicar ativos.
* As soluções personalizadas são criadas com base no código [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) base.
* [!DNL Experience Manager] [vincular ](/help/assets/link-sharing.md) compartilhamento para compartilhar ativos ad hoc usando links.
* [Interface da Web do Experience Manager Assets ](/help/assets/manage-assets.md) com áreas para terceiros externos protegidas pela configuração do controle de  [!DNL Experience Manager] acesso e com ajustes necessários de configuração de TI/rede, dando a esses usuários externos acesso ao  [!DNL Experience Manager].

## Principais conceitos e casos de uso {#key-concepts-and-use-cases}

### Glossário de termos comuns {#glossary-of-common-terms}

* **Trabalho em andamento ou trabalho criativo em andamento (WIP)**: uma fase no ciclo de vida do ativo em que um ativo sofre várias alterações e normalmente ainda não está pronto para ser compartilhado com equipes maiores.
* **Ativos prontos para criação:** [!DNL Assets]  que estão prontos para serem compartilhados com uma equipe maior ou que foram selecionados ou aprovados pela equipe criativa para compartilhamento com equipes de marketing ou LOB.
* **Aprovações de ativos**: o processo de aprovação que executa ativos já carregados no DAM, que normalmente inclui aprovações de marca, legais e assim por diante.
* **Ativo final**: um ativo que passou por todas as aprovações/marcações de metadados e está pronto para ser usado pela equipe maior. Esse ativo é armazenado no DAM e disponibilizado a todos os usuários (ou a todos os interessados). Ele pode ser usado em canais de marketing ou por equipes criativas para criar designs.
* **Atualização/alteração de ativos secundários:** uma pequena e rápida mudança em um ativo digital. Geralmente é feito em resposta a uma solicitação de retoque ou edição secundária, revisão de ativos ou aprovação (por exemplo, reposição, alteração do tamanho do texto, ajuste da saturação/brilho, cor e assim em diante).
* **Atualizações/alterações de ativos principais:** uma mudança em um ativo digital que requer trabalho considerável, e às vezes deve ser feita por um período mais longo. Normalmente, inclui várias alterações. O ativo deve ser salvo várias vezes durante a atualização. As atualizações de ativos principais normalmente fazem com que o ativo entre em um estágio WIP.
* **DAM:** Gerenciamento de ativos digitais. Neste documento, ele é sinônimo de [!DNL Experience Manager Assets], a menos que especificamente mencionado o contrário.
* **Usuário criativo**: um profissional criativo, que cria ativos digitais usando aplicativos e serviços da Creative Cloud. Em alguns casos, um usuário criativo pode ser membro de uma equipe criativa que pode usar a Creative Cloud, mas não cria ativos digitais (como um diretor criativo ou gerente de equipe criativa).
* **Usuário do DAM:** um usuário típico de um sistema DAM. Dependendo da organização, um usuário do DAM pode ser um usuário de marketing ou não, por exemplo, um usuário de Linha de Negócios (LOB), um bibliotecário, um vendedor e assim por diante.

### Considerações ao usar [!DNL Experience Manager] e [!DNL Creative Cloud] integração {#considerations-when-using-aem-and-creative-cloud-integration}

* Consulte [práticas recomendadas do aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)
* Consulte [Integração do Adobe Stock](aem-assets-adobe-stock.md)
* Consulte o [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Este é um breve resumo das práticas recomendadas para integração [!DNL Experience Manager] e [!DNL Creative Cloud]. Leia o resto deste documento para obter a compreensão detalhada sobre eles.

* **Para usuários criativos, que trabalham no Photoshop, InDesign ou Illustrator:** o do Adobe Asset Link fornece a melhor experiência do usuário, incluindo a manipulação limpa do Trabalho em andamento em ativos tirados do [!DNL Experience Manager].
* **Para simplificar o acesso a ativos do desktop para qualquer formato de arquivo ou aplicativo genérico:** use o aplicativo  [!DNL Experience Manager] de desktop.
* **Entenda por que e quando armazenar ativos no DAM:** atualizações a serem disponibilizadas para a equipe maior em sua organização.
* **Considere o volume de ativos compartilhados:** se o caso de uso for a distribuição de ativos, a governança e a segurança podem ser os aspectos mais importantes. Considere usar ferramentas criadas para fazer isso em escala, como o Brand Portal.
* **Entenda o ciclo de vida do ativo:** saiba como os ativos são manipulados em sua organização por equipes diferentes
* **Lidar com salvamentos frequentes em ativos com cuidado:** o Adobe Asset Link cuida disso para você com PS, AI, ID. Em outros aplicativos, não realize tarefas em andamento na pasta mapeada/compartilhada, a menos que precise de todas as alterações no DAM

### Acesso a [!DNL Adobe Stock] ativos de [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[A ](/help/assets/aem-assets-adobe-stock.md) integração do Experience Manager e Adobe Stock fornece  [!DNL Experience Manager] aos usuários a capacidade de pesquisar, visualizar, licenciar e salvar ativos do  [!DNL Adobe Stock] para  [!DNL Experience Manager]. Os ativos [!DNL Stock] licenciados e salvos selecionaram metadados [!DNL Stock], que podem ser usados para pesquisá-los com filtros extras.

Alguns pontos importantes sobre essa integração:

* Quando os ativos do Adobe stock são salvos em [!DNL Experience Manager], eles se tornam um [!DNL Assets] comum, com o binário salvo no repositório [!DNL Experience Manager]. Alguns metadados relacionados a [!DNL Adobe Stock] são salvos para o ativo em [!DNL Experience Manager], caso contrário, o processo de assimilação será igual ao de qualquer outro arquivo. Por exemplo, se as Tags inteligentes estiverem ativas, as tags serão adicionadas a esses ativos ao salvar.
* O ativo salvo em [!DNL Experience Manager] é uma cópia, não um link de volta em [!DNL Adobe Stock].

**Trabalhar com ativos salvos do  [!DNL Adobe Stock] em  [!DNL Experience Manager] no[!DNL Creative Cloud]**. Essa integração é independente de [!DNL Adobe Asset Link], mas [!DNL Adobe Asset Link] reconhece esses ativos salvos de [!DNL Stock] dessa forma, e exibe metadados adicionais e um logotipo [!DNL Adobe Stock] nesses ativos na interface do usuário de extensão [!DNL Adobe Asset Link] em [!DNL Photoshop], [!DNL Illustrator] ou [!DNL InDesign]. Os arquivos estão disponíveis para navegação, abertura e assim por diante, porque são ativos comuns quando salvos em [!DNL Experience Manager].
Os usuários criativos que trabalham em [!DNL Creative Cloud] aplicativos com extensão [!DNL Adobe Asset Link] presente, além de terem acesso a ativos já licenciados de [!DNL Adobe Stock] para [!DNL Experience Manager], também podem usar o painel Bibliotecas [!DNL Creative Cloud] para pesquisar, visualizar e licenciar ativos [!DNL Adobe Stock].
[!DNL Assets] de  [!DNL Adobe Stock] licenças e salvas em  [!DNL Experience Manager] tornam-se disponíveis para as equipes mais amplas que acessam a  [!DNL Experience Manager Assets] implantação, enquanto os ativos de licenciamento criativos  [!DNL Adobe Stock] por meio do painel  [!DNL Creative Cloud] Bibliotecas os os disponibilizam somente por padrão em suas  [!DNL Creative Cloud] contas.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Sobre o armazenamento de ativos em um DAM {#about-storing-assets-in-a-dam}

Para projetar um fluxo de trabalho eficiente entre equipes de criação e de marketing/linha de negócios (LOB) e escolher os melhores recursos de suporte, é importante entender quando e por que os ativos são armazenados no DAM.

### Por que os ativos são armazenados no DAM {#why-assets-are-stored-in-dam}

Armazenar ativos no DAM os torna facilmente acessíveis e acessíveis. Ela garante que os ativos possam ser aproveitados por vários usuários na organização ou no ecossistema, o que inclui parceiros, clientes e assim por diante.

A maioria das organizações opta por armazenar apenas ativos relevantes para os processos de marketing/LOB de downstream (publicação em canais como canal da Web via [!DNL Experience Manager Sites] ou outros canais fornecidos pelo Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e medidos pela Analytics Cloud, fornecendo a usuários/parceiros e assim por diante). Além disso, as organizações armazenam ativos que podem estar sujeitos a um processo de revisão/aprovação no DAM. Dessa forma, o DAM armazena principalmente ativos que têm altas chances de serem aproveitados e evita o armazenamento de ativos inativos.

O armazenamento de ativos também está sujeito a considerações técnicas e de utilização de recursos. O DAM fornece serviços adicionais sobre ativos armazenados, incluindo extração de metadados, controle de versão, geração de visualizações/transcodificação, gerenciamento de referências e adição de informações de controle de acesso. Esses serviços consomem mais tempo e recursos de infraestrutura.

Geralmente, o armazenamento de todos os ativos e atualizações não é desejável. Por exemplo, se as atualizações de ativos específicos forem de baixa qualidade e consumirem recursos excessivos, os ativos podem não ser armazenados no DAM.

#### Quando os ativos são armazenados no DAM {#when-assets-are-stored-in-dam}

Geralmente, as equipes criativas (e organizações) não estão interessadas em armazenar ativos em cada estágio do ciclo de vida do ativo. Por exemplo, eles evitam armazenar ativos nos seguintes casos:

* Ativos que ainda não foram finalizados ou estão sujeitos a experimentação.
* Ativos que não passam no ciclo de análise de criação/equipe interna.
* Em comparação com o ativo em questão, a equipe tem melhores candidatos para representar seu trabalho para equipes externas.

Normalmente, os seguintes ativos de classes são armazenados no DAM:

* Ativos que atingiram um determinado prazo e são considerados prontos para serem partilhados.
* Ativos pré-selecionados pela equipe criativa.
* Formatos de ativos específicos que podem ser usados ou solicitados pelo marketing, dependendo de um contrato ou contrato específico (por exemplo, arquivos JPG convertidos de arquivos RAW, TIFFs/imagens de originais PSD).

#### Quando as atualizações de ativos são armazenadas no DAM {#when-updates-to-assets-are-stored-in-dam}

Como regra, somente as atualizações de ativos relevantes para o conjunto mais amplo de usuários do DAM devem ser armazenadas no DAM. Isso garante que os usuários (marketing e funções semelhantes) visualizem apenas as versões relevantes na linha do tempo do ativo do DAM.

Normalmente, as alterações estão relacionadas aos marcos principais no ciclo de vida do ativo. Por exemplo, o ativo pronto para marketing ou uma atualização oficial com base na solicitação/revisão fornecida pela equipe criativa deve ser armazenado e ter controle de versão no DAM.

A atualização da equipe criativa para revisão pela equipe de marketing após uma solicitação de alteração do ativo existente no DAM é um exemplo de uma atualização relevante. Ele deve ser armazenado e ter controle de versão no DAM para referência adicional ou para reverter para a versão anterior.

A seguir estão exemplos de atualizações que normalmente não são relevantes:

* Versões anteriores dos ativos carregados antes de estarem prontos para análise de marketing
* Alterações criativas frequentes no ativo na fase de trabalho em andamento antes que as equipes criativas e de marketing decidam que o ativo está pronto

### Acesso do usuário ao DAM {#user-access-to-dam}

[!DNL Assets] O suporta dois tipos de usuários com base em seu acesso à  [!DNL Assets] implantação. Normalmente, os usuários dentro da rede corporativa (firewall) têm acesso direto ao DAM. Outros utilizadores fora da rede empresarial não teriam acesso direto. O tipo de usuário determina quais integrações podem ser usadas do ponto de vista técnico.

#### Usuários criativos com acesso direto ao DAM {#creative-users-with-direct-access-to-dam}

Normalmente, as equipes criativas internas ou os profissionais de criação integrados à rede interna têm acesso à implantação do DAM, incluindo o logon [!DNL Experience Manager]. [!DNL Experience Manager] A infraestrutura de rede e pode ser configurada para permitir acesso direto a partes externas - geralmente organizações confiáveis como agências que trabalham para um cliente - para ter acesso a  [!DNL Experience Manager] pela rede, por exemplo, via VPN ou lista de permissões IP.

Nesses casos, o Adobe Asset Link ou o aplicativo de desktop [!DNL Experience Manager] ajuda a fornecer acesso fácil a ativos finais/aprovados e permite salvar ativos prontos para criação no DAM.

#### Usuários criativos sem acesso ao DAM {#creative-users-without-access-to-dam}

Agências externas e freelancers sem acesso direto à implantação do DAM podem exigir acesso a ativos aprovados ou desejar adicionar seus novos designs ao DAM.

Use as seguintes estratégias para fornecer acesso a ativos finais/aprovados:

* Use o aplicativo de desktop se o Asset Link não funcionar.
* Use [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para distribuir ativos com segurança para parceiros externos
* Use uma implementação personalizada de um portal de distribuição e fornecimento com base em [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Use o Controle de Acesso configurado em [!DNL Experience Manager] e a infraestrutura de rede necessária (por exemplo, VPN e lista de permissões de IP) para conceder acesso a partes externas a uma área dedicada de conteúdo no DAM. Eles podem usar [!DNL Experience Manager] Interface do usuário da Web para obter ativos e carregar novo conteúdo no DAM.

#### Trabalho em andamento em ativos de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Conforme discutido neste documento, é recomendável realizar atualizações importantes em ativos, às vezes chamados de trabalho em andamento, sem ter todas as edições salvas no arquivo local também carregadas para [!DNL Experience Manager] como alterações. Isso acelera o trabalho de um usuário de desktop, limita a largura de banda da rede usada e mantém a linha do tempo dos ativos limpa e focada em atualizações importantes e controladas.

O Adobe Asset Link oferece um bom suporte para este caso de uso:

* Quando os usuários em [!DNL Photoshop], [!DNL InDesign] ou [!DNL Illustrator] pretendem editar um arquivo, eles executam uma operação de Check-out no ativo em questão
* O ativo é baixado em segundo plano, colocado na conta do Creative Cloud de usuários sincronizada ao disco pelo aplicativo de desktop do Creative Cloud e o sinalizador de check-out é alternado em [!DNL Experience Manager] no ativo para minimizar conflitos de edição
* A partir daí, o usuário trabalha em um arquivo armazenado localmente no local sincronizado e pode continuar trabalhando e salvando as alterações necessárias a qualquer frequência necessária
* Além disso, como o ativo está na conta do Creative Cloud, ele também está disponível em outros dispositivos que o usuário pode ter (por exemplo, pode ser aberto ou editado em um aplicativo móvel Creative Cloud dedicado) e pode ser compartilhado com outros usuários do Creative Cloud para fins de colaboração.
* Quando o usuário criativo terminar com as alterações, ele poderá executar uma operação de Check-in nesse arquivo em seu aplicativo Creative Cloud, com um comentário opcional. O ativo correspondente em [!DNL Experience Manager] tem controle de versão e é atualizado para com o novo binário. [!DNL Experience Manager] usuários como profissionais de marketing ou usuários de LOB têm acesso a grandes alterações de ativos ou marcos, por meio da interface do usuário da linha do tempo  [!DNL Experience Manager] de ativos.

[!DNL Experience Manager] o aplicativo de desktop fornece um compartilhamento de rede para ativos abertos no aplicativo nativo. Por padrão, todas as alterações feitas localmente são carregadas automaticamente para [!DNL Experience Manager] após um breve período. Com essa configuração, salvas frequentes durante a fase de trabalho em andamento seriam carregadas em [!DNL Experience Manager] e com versão, criando muito tráfego de rede e possíveis desafios de escalabilidade - para não mencionar versões desnecessárias em [!DNL Experience Manager].

A abordagem recomendada aqui é usar uma opção no [!DNL Experience Manager] aplicativo de desktop para desativar atualizações automatizadas e fazer upload de alterações em ativos para [!DNL Experience Manager] manualmente, aproveitando a ação de upload de alterações na interface do usuário de status de ativos do aplicativo.

#### Upload em massa no DAM {#bulk-upload-to-dam}

Você pode ter um requisito para fazer upload simultâneo de um número maior de arquivos no DAM em alguns cenários, por exemplo:

* Upload de resultados de fotos ou projetos maiores
* Upload de ativos fornecidos por agências criativas
* Fazer upload dos ativos selecionados de um conjunto maior se a seleção for feita fora do DAM

A descrição se refere ao upload de arquivos operacionalmente (por exemplo, toda semana ou com cada sessão fotográfica), como parte normal do fluxo de trabalho do usuário do desktop. As migrações de ativos grandes não são contempladas aqui.

Você pode aproveitar os seguintes recursos de upload:

* Para fazer upload de pastas grandes/hierárquicas em massa, use o [!DNL Experience Manager] aplicativo de desktop que fornece a funcionalidade [upload de pasta](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem). Também é possível fazer upload de estruturas hierárquicas de pastas. [!DNL Assets] são carregadas em segundo plano e, portanto, não estão vinculadas a uma sessão do navegador da Web
* Para carregar alguns arquivos de uma única pasta, arraste os arquivos diretamente para a interface da Web ou use a opção Criar na interface da Web [!DNL Assets].
* Dependendo dos requisitos de sua empresa, você também pode usar o carregador personalizado.

#### Gerenciar ativos digitais diretamente do desktop {#managing-digital-assets-directly-from-desktop}

Se você usar os Compartilhamentos de arquivo de rede para gerenciar ativos digitais, apenas o uso do compartilhamento de rede mapeado pelo aplicativo de desktop [!DNL Experience Manager] pode ser visto como um substituto conveniente. Ao fazer a transição dos compartilhamentos de arquivos de rede, a [!DNL Experience Manager] interface da Web fornece um conjunto avançado de recursos de Gerenciamento de ativos digitais que vai muito além do que é possível em um compartilhamento de rede (pesquisa, coleções, metadados, colaboração, visualizações e assim por diante), e o [!DNL Experience Manager] aplicativo de desktop fornece um link útil para conectar o repositório DAM do lado do servidor ao trabalho no desktop.

Evite usar [!DNL Experience Manager] aplicativo de desktop para gerenciar ativos diretamente no compartilhamento de rede de [!DNL Assets]. Por exemplo, evite usar [!DNL Experience Manager] aplicativo de desktop para mover/copiar vários arquivos. Em vez disso, use a interface [!DNL Assets] para arrastar as pastas do Localizador/Explorer para o compartilhamento de rede ou use o recurso [!DNL Assets] Upload de pasta.

#### Migração de ativos {#asset-migration}

Para planejar e executar as migrações de ativos do sistema existente para um novo sistema ou a migração de um grande volume de ativos armazenados em servidores, consulte o [Guia de Migração](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] o aplicativo de desktop e  [!DNL Experience Manager] as  [!DNL Creative Cloud] integrações não são compatíveis com essas migrações. Devido aos grandes volumes de ativos a serem assimilados e aos requisitos adicionais sobre mapeamento, transformação e assimilação de metadados, as migrações devem ser tratadas usando diferentes ferramentas e abordagens.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Práticas recomendadas para aplicativos de desktop do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integração do Experience Manager e Adobe Stock](aem-assets-adobe-stock.md)


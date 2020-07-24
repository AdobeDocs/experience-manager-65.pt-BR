---
title: Adobe Experience Manager para as práticas recomendadas de compartilhamento de pastas da Adobe Creative Cloud
description: Configure o Adobe Experience Manager para permitir que os usuários do Experience Manager Assets troquem pastas com usuários da Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---


# Adobe Experience Manager para compartilhamento de pastas da Adobe Creative Cloud {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>O recurso Experience Manager para compartilhamento de pastas da Creative Cloud está obsoleto. A Adobe recomenda usar recursos mais recentes, como o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) ou o aplicativo [de desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)Experience Manager. Saiba mais sobre as práticas [recomendadas de integração da](/help/assets/aem-cc-integration-best-practices.md)Experience Manager e da Creative Cloud.

O Adobe Experience Manager pode ser configurado para permitir que os usuários do Assets compartilhem pastas com os usuários dos aplicativos da Adobe Creative Cloud, de modo que eles estejam disponíveis como pastas compartilhadas no serviço Adobe Creative Cloud Assets. O recurso pode ser usado para trocar arquivos entre equipes de criação e usuários do Assets, especialmente quando os usuários criativos não têm acesso à implantação do Assets (eles não estão na rede corporativa).

Esse tipo de integração pode ser usado nos seguintes casos de uso, especialmente ao trabalhar com usuários que não têm acesso direto aos Ativos:

* Os usuários do Assets compartilham um conjunto de ativos específicos com os usuários dos arquivos da Adobe Creative Cloud (por exemplo, um resumo criativo e um conjunto de ativos aprovados para o trabalho de design de uma nova atividade de marketing)
* Os usuários do Assets recebem novos arquivos criados pelos usuários do aplicativo Adobe Creative Cloud.

>[!NOTE]
>
>Antes de ler este documento, você pode consultar as práticas [recomendadas gerais de integração da](/help/assets/aem-cc-integration-best-practices.md) Experience Manager e da Creative Cloud para obter uma visão geral de nível superior do tópico.

## Visão geral {#overview}

O Experience Manager para o compartilhamento de pastas da Creative Cloud depende do compartilhamento no servidor de pastas e arquivos entre as contas do Assets e da Creative Cloud. Os profissionais da Creative Cloud, que usam o aplicativo de desktop da Creative Cloud em seus desktops, podem disponibilizar as pastas compartilhadas diretamente em seus discos usando a tecnologia Adobe CreativeSync.

O diagrama a seguir fornece uma visão geral da integração.

![chlimage_1-179](assets/chlimage_1-406.png)

A integração inclui os seguintes elementos:

* **Servidor** do Experience Manager Assets implantado na rede corporativa (serviços gerenciados ou no local): O compartilhamento de pastas é iniciado aqui.
* **Serviço** principal do Adobe Marketing Cloud Assets: Atua como intermediário entre os serviços de armazenamento da Experience Manager e da Creative Cloud. O administrador da empresa que usa a integração precisa estabelecer uma relação de confiança entre a organização da Marketing Cloud e a implantação dos Ativos. Eles também [definem uma lista de colaboradores](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)aprovados da Creative Cloud, que os usuários do Assets também podem compartilhar pastas para segurança adicional.

* **Serviços** da Web do Creative Cloud Assets (interface do usuário da Web de arquivos do armazenamento e da Creative Cloud): É aqui que usuários específicos do aplicativo da Creative Cloud, com quem uma pasta Ativos foi compartilhada, poderão aceitar o convite e ver a pasta em seu armazenamento de conta da Creative Cloud.
* **Aplicativo** de desktop da Creative Cloud: (Opcional) Permite acesso direto a pastas/arquivos compartilhados da área de trabalho do usuário criativo por meio da sincronização com o armazenamento Creative Cloud Assets.

## Características e limitações {#characteristics-and-limitations}

* **Propagação unidirecional das alterações:** As alterações de arquivo são propagadas em uma única direção - do sistema (Experience Manager ou Creative Cloud Assets), onde o ativo foi criado originalmente (carregado). A integração não fornece uma sincronização bidirecional totalmente automatizada entre os dois sistemas.
* **Versões:**

   * O Experience Manager só cria versões de um ativo em atualizações se o arquivo tiver origem no Experience Manager e for atualizado nele.
   * A Creative Cloud Assets fornece seu próprio recurso [de](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) controle de versão direcionado para atualizações do Work in Progress (basicamente, armazena atualizações por até 10 dias)

* **Limitações de espaço:** Os tamanhos e volumes de arquivos trocados são limitados pela cota [específica de ativos da](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud para usuários criativos (depende do nível de subscrição) e por uma limitação de 5 GB do tamanho máximo de arquivos. O espaço é adicionalmente limitado pela cota de ativos que a organização tem no serviço principal do Adobe Marketing Cloud Assets.

* **Requisitos de espaço:** Os arquivos em pastas compartilhadas também precisam ser armazenados fisicamente no Experience Manager e, em seguida, na conta da Creative Cloud, com uma cópia em cache no serviço principal dos Ativos da Marketing Cloud.
* **Rede e largura de banda:** Os arquivos em pastas compartilhadas e todas as atualizações precisam ser transportados pela rede entre os sistemas. Você deve garantir que somente os arquivos e as atualizações relevantes sejam compartilhados.
* **Tipo** de pasta: O compartilhamento de uma pasta Assets do tipo `sling:OrderedFolder`não é suportado no contexto do compartilhamento no Adobe Marketing Cloud. Se desejar compartilhar uma pasta, ao criá-la em Ativos, não selecione a opção Solicitado.

## Best practices {#best-practices}

As práticas recomendadas para aproveitar o Experience Manager para o compartilhamento de pastas da Creative Cloud incluem:

* **Considerações sobre volume:** O Compartilhamento de pastas da Experience Manager/Creative Cloud deve ser usado para compartilhar um número menor de arquivos, por exemplo, relevantes para uma campanha ou atividade específica. Para compartilhar conjuntos maiores de ativos, como todos os ativos aprovados na organização, use outros métodos de distribuição (por exemplo, o Portal de marcas do Assets) ou o aplicativo de desktop Experience Manager.

* **Evite compartilhar hierarquias profundas:** O compartilhamento funciona recursivamente e não permite o compartilhamento seletivo. Normalmente, somente pastas sem subpastas ou com uma hierarquia muito superficial, como 1 nível de subpasta, devem ser consideradas para compartilhamento.
* **Separe pastas para compartilhamento unidirecional:** Pastas separadas devem ser usadas para compartilhar ativos finais de Ativos em arquivos da Creative Cloud e para compartilhar ativos prontos para criação de volta de arquivos da Creative Cloud para os Ativos. Junto com uma boa convenção de nomenclatura para essas pastas, ela cria um ambiente de trabalho mais fácil de entender para os usuários do Assets e da Creative Cloud.
* **Evite o WIP na pasta compartilhada:** A pasta compartilhada não deve ser usada para o Trabalho em andamento - use uma pasta separada na Creative Cloud Files para realizar um trabalho que exija alterações frequentes no arquivo.
* **Start do novo trabalho fora da pasta compartilhada:** Os novos designs (arquivos criativos) devem ser iniciados na pasta WIP separada nos Arquivos da Creative Cloud e, quando estiverem prontos para serem compartilhados com os usuários do Assets, devem ser movidos ou salvos na pasta compartilhada.
* **Simplifique a estrutura de compartilhamento:** Para uma configuração operacional mais gerenciável, pense em simplificar a estrutura de compartilhamento. Em vez de compartilhar com todos os usuários criativos, as pastas Ativos devem ser compartilhadas somente com representantes da equipe, como um diretor criativo ou um gerente de equipe. O gerente do lado criativo receberá ativos finais, decidirá sobre atribuições de trabalho e permitirá que os designers trabalhem em suas próprias contas da Creative Cloud em ativos WIP. Eles podem usar os recursos de colaboração da Creative Cloud para coordenar o trabalho e, por fim, selecionar e colocar ativos prontos para compartilhar de volta aos Ativos em sua pasta compartilhada pronta para criação.

O diagrama a seguir ilustra um exemplo de configuração para a criação de novos designs com base nos ativos finais existentes do Assets.

![chlimage_1-180](assets/chlimage_1-407.png)

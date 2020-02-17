---
title: Práticas recomendadas de compartilhamento de pastas do AEM para a Creative Cloud
description: Configure o Adobe Experience Manager (AEM) para permitir que os usuários do AEM Assets troquem pastas com usuários da Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Práticas recomendadas de compartilhamento de pastas do AEM para a Creative Cloud {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>O recurso Compartilhamento de pastas do AEM para a Creative Cloud está obsoleto. A Adobe recomenda usar recursos mais recentes, como o [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) ou o aplicativo [de desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)AEM. Saiba mais sobre as práticas [recomendadas de integração do](/help/assets/aem-cc-integration-best-practices.md)AEM e da Creative Cloud.

O Adobe Experience Manager (AEM) pode ser configurado para permitir que os usuários do AEM Assets compartilhem pastas com os usuários dos aplicativos da Adobe Creative Cloud, de modo que eles estejam disponíveis como pastas compartilhadas no serviço Adobe Creative Cloud Assets. O recurso pode ser usado para trocar arquivos entre equipes de criação e usuários do AEM Assets, especialmente quando os usuários criativos não têm acesso à instância do AEM Assets (eles não estão na rede corporativa).

Esse tipo de integração pode ser usado nos seguintes casos de uso, especialmente ao trabalhar com usuários que não têm acesso direto aos ativos AEM:

* Os usuários do AEM Assets compartilham um conjunto de ativos específicos com usuários dos arquivos da Adobe Creative Cloud (por exemplo, um resumo criativo e um conjunto de ativos aprovados para o trabalho de design de uma nova atividade de marketing)
* Os usuários do AEM Assets recebem novos arquivos criados por usuários de aplicativos da Adobe Creative Cloud.

>[!NOTE]
>
>Antes de ler este documento, você pode consultar as práticas [recomendadas gerais de integração do](/help/assets/aem-cc-integration-best-practices.md) AEM e da Creative Cloud para obter uma visão geral de nível superior do tópico.

## Visão geral {#overview}

O compartilhamento de pastas do AEM para a Creative Cloud depende do compartilhamento de pastas e arquivos no servidor entre os ativos AEM e as contas da Creative Cloud. Os profissionais da Creative Cloud, que usam o aplicativo de desktop da Creative Cloud em seus desktops, podem disponibilizar as pastas compartilhadas diretamente em seus discos usando a tecnologia Adobe CreativeSync.

O diagrama a seguir fornece uma visão geral da integração.

![chlimage_1-179](assets/chlimage_1-406.png)

A integração inclui os seguintes elementos:

* **Servidor** do AEM Assets implantado na rede corporativa (serviços gerenciados ou no local): O compartilhamento de pastas é iniciado aqui.
* **Serviço** principal do Adobe Marketing Cloud Assets: Atua como intermediário entre os serviços de armazenamento do AEM e da Creative Cloud. O administrador da empresa que usa a integração precisa estabelecer uma relação de confiança entre a organização da Marketing Cloud e a instância do AEM Assets. Eles também [definem uma lista de colaboradores](https://marketing.adobe.com/resources/help/en_US/mcloud/t_admin_add_cc_user.html)aprovados da Creative Cloud, que os usuários do AEM Assets também podem compartilhar pastas para segurança adicional.

* **Serviços** da Web do Creative Cloud Assets (armazenamento e interface do usuário da Web dos arquivos da Creative Cloud): É aqui que usuários específicos do aplicativo da Creative Cloud, com quem uma pasta dos ativos AEM foi compartilhada, poderão aceitar o convite e ver a pasta em seu armazenamento de conta da Creative Cloud.
* **Aplicativo** de desktop da Creative Cloud: (Opcional) Permite acesso direto a pastas compartilhadas/arquivos da área de trabalho do usuário criativo por meio da sincronização com o armazenamento da Creative Cloud Assets.

## Características e limitações {#characteristics-and-limitations}

* **** Propagação unidirecional das alterações: As alterações de arquivo são propagadas em uma única direção - do sistema (AEM ou Creative Cloud Assets), onde o ativo foi criado originalmente (carregado). A integração não fornece uma sincronização bidirecional totalmente automatizada entre os dois sistemas.
* **Versões:**

   * O AEM só cria versões de um ativo em atualizações se o arquivo tiver origem no AEM e for atualizado nele.
   * A Creative Cloud Assets fornece seu próprio recurso [de](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) controle de versão direcionado para atualizações do Work in Progress (basicamente, armazena atualizações por até 10 dias)

* **** Limitações de espaço: Os tamanhos e volumes de arquivos trocados são limitados pela cota [específica de ativos da](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud para usuários criativos (depende do nível de assinatura) e por uma limitação de 5 GB do tamanho máximo de arquivos. O espaço é ainda limitado pela cota de ativos que a organização tem no serviço principal do Adobe Marketing Cloud Assets.

* **** Requisitos de espaço: Os arquivos em pastas compartilhadas também precisam ser armazenados fisicamente no AEM e depois na conta da Creative Cloud, com uma cópia em cache no serviço principal dos Ativos da Marketing Cloud.
* **** Rede e largura de banda: Os arquivos em pastas compartilhadas e todas as atualizações precisam ser transportados pela rede entre os sistemas. Você deve garantir que somente os arquivos e as atualizações relevantes sejam compartilhados.
* **Tipo** de pasta: O compartilhamento de uma pasta Ativos do tipo `sling:OrderedFolder`não é suportado no contexto do compartilhamento na Adobe Marketing Cloud. Se desejar compartilhar uma pasta, ao criá-la nos ativos AEM, não selecione a opção Solicitado.

## Best practices {#best-practices}

As práticas recomendadas para aproveitar o compartilhamento de pastas do AEM para a Creative Cloud incluem:

* **** Considerações sobre volume: O compartilhamento de pastas do AEM/Creative Cloud deve ser usado para compartilhar um número menor de arquivos, por exemplo, relevantes para uma campanha ou atividade específica. Para compartilhar conjuntos maiores de ativos, como todos os ativos aprovados na organização, use outros métodos de distribuição (por exemplo, o AEM Assets Brand Portal) ou o aplicativo de desktop do AEM.

* **** Evite compartilhar hierarquias profundas: O compartilhamento funciona recursivamente e não permite o compartilhamento seletivo. Normalmente, somente pastas sem subpastas ou com uma hierarquia muito superficial, como 1 nível de subpasta, devem ser consideradas para compartilhamento.
* **** Separe pastas para compartilhamento unidirecional: Pastas separadas devem ser usadas para compartilhar ativos finais dos ativos AEM para arquivos da Creative Cloud e para compartilhar ativos prontos para criação de volta dos arquivos da Creative Cloud para os ativos AEM. Junto com uma boa convenção de nomenclatura para essas pastas, ela cria um ambiente de trabalho mais fácil de entender para os ativos AEM e usuários da Creative Cloud.
* **** Evite o WIP na pasta compartilhada: A pasta compartilhada não deve ser usada para o Trabalho em andamento - use uma pasta separada na Creative Cloud Files para realizar um trabalho que exija alterações frequentes no arquivo.
* **** Iniciar novo trabalho fora da pasta compartilhada: Os novos designs (arquivos criativos) devem ser iniciados na pasta WIP separada em Arquivos da Creative Cloud e, quando estiverem prontos para serem compartilhados com usuários do AEM Assets, devem ser movidos ou salvos na pasta compartilhada.
* **** Simplifique a estrutura de compartilhamento: Para uma configuração operacional mais gerenciável, pense em simplificar a estrutura de compartilhamento. Em vez de compartilhar com todos os usuários criativos, as pastas do AEM Assets devem ser compartilhadas somente com representantes da equipe, como um diretor criativo ou um gerente de equipe. O gerente do lado criativo receberá ativos finais, decidirá sobre atribuições de trabalho e permitirá que os designers trabalhem em suas próprias contas da Creative Cloud em ativos WIP. Eles podem usar os recursos de colaboração da Creative Cloud para coordenar o trabalho e, por fim, selecionar e colocar ativos prontos para compartilhamento nos ativos AEM na pasta compartilhada pronta para criação.

O diagrama a seguir ilustra um exemplo de configuração para criar novos designs com base nos ativos finais existentes dos ativos AEM.

![chlimage_1-180](assets/chlimage_1-407.png)

---
title: Práticas de teste [!DNL Adobe Creative Cloud] de compartilhamento de pastas
description: Configure [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] para trocar pastas com usuários do Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] para compartilhamento de [!DNL Adobe Creative Cloud] pastas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>O recurso Compartilhamento [!DNL Experience Manager] para [!DNL Creative Cloud] pasta está obsoleto. A Adobe recomenda usar recursos mais recentes, como o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) ou o aplicativo [de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)Experience Manager. Saiba mais sobre as práticas [recomendadas de integração de](/help/assets/aem-cc-integration-best-practices.md)Experience Manager e Creative Cloud.

[!DNL Adobe Experience Manager] pode ser configurado para permitir que os usuários compartilhem pastas com [!DNL Assets] os usuários dos [!DNL Adobe Creative Cloud] aplicativos, de modo que eles estejam disponíveis como pastas compartilhadas no serviço de [!DNL Adobe Creative Cloud] ativos. O recurso pode ser usado para trocar arquivos entre equipes de criação e [!DNL Assets] usuários, especialmente quando os usuários criativos não têm acesso à [!DNL Assets] implantação (eles não estão na rede corporativa).

Esse tipo de integração pode ser usado nos seguintes casos de uso, especialmente ao trabalhar com usuários que não têm acesso direto a [!DNL Assets]:

* [!DNL Assets] os usuários compartilham um conjunto de ativos digitais específicos com usuários de [!DNL Adobe Creative Cloud] arquivos (por exemplo, um resumo criativo e um conjunto de ativos aprovados para o trabalho de design de uma nova atividade de marketing).
* [!DNL Assets] os usuários recebem novos arquivos criados pelos usuários do [!DNL Adobe Creative Cloud] aplicativo.

>[!NOTE]
>
>Antes de ler este documento, você pode consultar as práticas [recomendadas gerais de integração de](/help/assets/aem-cc-integration-best-practices.md) Experience Manager e Creative Cloud para obter uma visão geral da integração.

## Visão geral {#overview}

[!DNL Experience Manager] o compartilhamento de [!DNL Creative Cloud] pastas depende do compartilhamento de pastas e arquivos entre [!DNL Assets] e [!DNL Creative Cloud] contas pelo lado do servidor. Profissionais criativos, que usam o aplicativo de [!DNL Creative Cloud] desktop em seus desktops, podem disponibilizar as pastas compartilhadas diretamente em seus discos usando a [!DNL Adobe CreativeSync] tecnologia.

O diagrama a seguir fornece uma visão geral da integração.

![chlimage_1-179](assets/chlimage_1-406.png)

A integração inclui os seguintes elementos:

* **[!DNL Experience Manager Assets]** implantado na rede corporativa (serviços gerenciados ou no local): O compartilhamento de pastas é iniciado aqui.
* **[!DNL Adobe Marketing Cloud Assets]serviço** principal: Atua como intermediário entre serviços [!DNL Experience Manager] e serviços [!DNL Creative Cloud] armazenamentos. Um administrador de uma organização que usa a integração precisa estabelecer uma relação de confiança entre a organização do Marketing Cloud e a [!DNL Assets] implantação. Eles também [definem uma lista de colaboradores](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)aprovados para Creative Cloud, que [!DNL Assets] os usuários também podem compartilhar pastas para segurança adicional.

* **[!DNL Creative Cloud]Serviços** da Web de ativos (UI da Web de armazenamentos e [!DNL Creative Cloud] arquivos): É aqui que usuários específicos do aplicativo Creative Cloud, com quem uma [!DNL Assets] pasta foi compartilhada, poderão aceitar o convite e ver a pasta em seu armazenamento de conta Creative Cloud.
* **Aplicativo** para desktop Creative Cloud: (Opcional) Permite acesso direto a pastas compartilhadas/arquivos da área de trabalho do usuário criativo por meio da sincronização com o armazenamento [!DNL Creative Cloud] Ativos.

## Características e limitações {#characteristics-and-limitations}

* **Propagação unidirecional das alterações:** As alterações de arquivo são propagadas em uma única direção - do sistema ([!DNL Experience Manager] ou [!DNL Creative Cloud Assets]), onde o ativo foi criado originalmente (carregado). A integração não fornece uma sincronização bidirecional totalmente automatizada entre os dois sistemas.
* **Versões:**

   * [!DNL Experience Manager] cria somente versões de um ativo em atualizações se o arquivo tiver se originado [!DNL Experience Manager] e for atualizado nele.
   * [!DNL Creative Cloud] O Assets fornece seu próprio recurso [de](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) controle de versão direcionado para atualizações do Work in Progress (basicamente, armazena atualizações por até 10 dias)

* **Limitações de espaço:** Os tamanhos e volumes de arquivos trocados são limitados pela cota [específica do](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud Assets para usuários criativos (depende do nível de subscrição) e por uma limitação de 5 GB do tamanho máximo do arquivo. O espaço é adicionalmente limitado pela cota de ativos que a organização tem no serviço principal do Adobe Marketing Cloud Assets.

* **Requisitos de espaço:** Os arquivos em pastas compartilhadas também precisam ser armazenados fisicamente na [!DNL Experience Manager] e depois na [!DNL Creative Cloud] conta, com uma cópia em cache no serviço [!DNL Marketing Cloud Assets] principal.
* **Rede e largura de banda:** Os arquivos em pastas compartilhadas e todas as atualizações precisam ser transportados pela rede entre os sistemas. Você deve garantir que somente os arquivos e as atualizações relevantes sejam compartilhados.
* **Tipo** de pasta: O compartilhamento de uma [!DNL Assets] pasta do tipo `sling:OrderedFolder`não é suportado no contexto do compartilhamento em [!DNL Adobe Marketing Cloud]. Se desejar compartilhar uma pasta, ao criá-la em [!DNL Assets], não selecione a opção [!UICONTROL Solicitado] .

## Best practices {#best-practices}

As práticas recomendadas para aproveitar o compartilhamento de pastas [!DNL Experience Manager] para [!DNL Creative Cloud] :

* **Considerações sobre volume:** [!DNL Experience Manager] e [!DNL Creative Cloud] o Compartilhamento de pastas deve ser usado para compartilhar um número menor de arquivos, por exemplo, relevantes para uma campanha ou atividade específica. Para compartilhar conjuntos maiores de ativos, como todos os ativos aprovados na organização, use outros métodos de distribuição (por exemplo, [!DNL Assets Brand Portal]) ou aplicativo de [!DNL Experience Manager] desktop.
* **Evite compartilhar hierarquias profundas:** O compartilhamento funciona recursivamente e não permite o compartilhamento seletivo. Normalmente, somente pastas sem subpastas ou com uma hierarquia muito superficial, como 1 nível de subpasta, devem ser consideradas para compartilhamento.
* **Separe pastas para compartilhamento unidirecional:** Pastas separadas devem ser usadas para compartilhar ativos finais de [!DNL Assets] a [!DNL Creative Cloud] arquivos e para compartilhar ativos prontos para criação de volta de [!DNL Creative Cloud] arquivos para [!DNL Assets]. Juntamente com uma boa convenção de nomenclatura para essas pastas, ela cria um ambiente de trabalho mais fácil de entender para [!DNL Assets] e para [!DNL Creative Cloud] os usuários.
* **Evite o WIP na pasta compartilhada:** A pasta compartilhada não deve ser usada para o Trabalho em andamento - use uma pasta separada em Arquivos de Creative Cloud para realizar um trabalho que exija alterações frequentes no arquivo.
* **Start do novo trabalho fora da pasta compartilhada:** Os novos designs (arquivos criativos) devem ser iniciados na pasta WIP separada em Arquivos de Creative Cloud e, quando estiverem prontos para serem compartilhados com [!DNL Assets] os usuários, devem ser movidos ou salvos na pasta compartilhada.
* **Simplifique a estrutura de compartilhamento:** Para uma configuração operacional mais gerenciável, pense em simplificar a estrutura de compartilhamento. Em vez de compartilhar com todos os usuários criativos, [!DNL Assets] as pastas devem ser compartilhadas somente com os representantes da equipe, como um diretor criativo ou um gerente de equipe. O gerente do lado criativo receberia ativos finais, decidiria sobre atribuições de trabalho e deixaria os designers trabalharem em suas próprias contas de Creative Cloud nos ativos WIP. Eles podem usar os recursos de colaboração Creative Cloud para coordenar o trabalho e, por fim, selecionar e colocar ativos prontos para compartilhar de volta em sua pasta compartilhada pronta para criação. [!DNL Assets]

O diagrama a seguir ilustra um exemplo de configuração para a criação de novos designs com base nos ativos finais existentes do [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)

---
title: Compartilhamento de pasta para  [!DNL Adobe Creative Cloud] práticas recomendadas
description: Configure [!DNL Adobe Experience Manager] para permitir que usuários em [!DNL Experience Manager Assets] troquem pastas com usuários do Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] para [!DNL Adobe Creative Cloud] compartilhamento de pastas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>O recurso Compartilhamento de Pastas de [!DNL Experience Manager] a [!DNL Creative Cloud] está obsoleto. O Adobe recomenda usar recursos mais recentes, como o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) ou o [Experience Manager desktop app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Saiba mais sobre as [práticas recomendadas de integração de Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

O [!DNL Adobe Experience Manager] pode ser configurado para permitir que os usuários no [!DNL Assets] compartilhem pastas com os usuários dos aplicativos [!DNL Adobe Creative Cloud], de modo que estejam disponíveis como pastas compartilhadas no serviço de ativos do [!DNL Adobe Creative Cloud]. O recurso pode ser usado para troca de arquivos entre equipes criativas e usuários do [!DNL Assets], especialmente quando os usuários criativos não têm acesso à implantação do [!DNL Assets] (eles não estão na rede corporativa).

Esse tipo de integração pode ser usado nos seguintes casos de uso, especialmente ao trabalhar com usuários que não têm acesso direto ao [!DNL Assets]:

* [!DNL Assets] usuários compartilham um conjunto de ativos digitais específicos com usuários de [!DNL Adobe Creative Cloud] arquivos (por exemplo, um resumo criativo e um conjunto de ativos aprovados para trabalho de design para uma nova atividade de marketing).
* [!DNL Assets] usuários recebem os novos arquivos criados por [!DNL Adobe Creative Cloud] usuários do aplicativo.

>[!NOTE]
>
>Antes de ler este documento, você pode consultar as [práticas recomendadas de integração de Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obter uma visão geral da integração.

## Visão geral {#overview}

O compartilhamento de pastas de [!DNL Experience Manager] para [!DNL Creative Cloud] depende do compartilhamento de pastas e arquivos do lado do servidor entre contas [!DNL Assets] e [!DNL Creative Cloud]. Os profissionais criativos, que usam o aplicativo de desktop [!DNL Creative Cloud] em seus desktops, também podem disponibilizar as pastas compartilhadas diretamente em seus discos usando a tecnologia [!DNL Adobe CreativeSync].

O diagrama a seguir fornece uma visão geral da integração.

![chlimage_1-179](assets/chlimage_1-406.png)

A integração inclui os seguintes elementos:

* **[!DNL Experience Manager Assets]** implantado na rede corporativa (Managed Services ou local): o compartilhamento de pastas é iniciado aqui.
* **[!DNL Adobe Experience Cloud Assets]serviço principal**: atua como um intermediário entre os serviços de armazenamento [!DNL Experience Manager] e [!DNL Creative Cloud]. Um administrador de uma organização que usa a integração deve estabelecer uma relação de confiança entre a organização Experience Cloud e a implantação do [!DNL Assets]. Eles também [definem uma lista de colaboradores de Creative Cloud aprovados](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html), para que os usuários do [!DNL Assets] também possam compartilhar pastas para segurança adicional.

* **[!DNL Creative Cloud]serviços Web do Assets** (armazenamento e interface da Web de [!DNL Creative Cloud] arquivos): é aqui que usuários específicos do aplicativo Creative Cloud, com os quais uma pasta [!DNL Assets] foi compartilhada, poderiam aceitar o convite e ver a pasta em seu armazenamento da conta Creative Cloud.
* **aplicativo de desktop Creative Cloud**: (opcional) permite acesso direto a pastas/arquivos compartilhados do desktop do usuário criativo por meio da sincronização com o armazenamento do Assets [!DNL Creative Cloud].

## Características e limitações {#characteristics-and-limitations}

* **Propagação unidirecional de alterações:** As alterações de arquivo são propagadas em uma única direção - do sistema ([!DNL Experience Manager] ou [!DNL Creative Cloud Assets]), onde o ativo foi criado originalmente (carregado). A integração não fornece uma sincronização bidirecional totalmente automatizada entre os dois sistemas.
* **Controle de Versão:**

   * O [!DNL Experience Manager] só criará versões de um ativo em atualizações se o arquivo tiver origem no [!DNL Experience Manager] e for atualizado nesse local.
   * [!DNL Creative Cloud] O Assets fornece seu próprio [recurso de controle de versão](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) direcionado para atualizações de Trabalho em Andamento (basicamente, armazena atualizações por até dez dias)

* **Limitações de espaço:** Os tamanhos e volumes de arquivos trocados são limitados pela [cota de Creative Cloud Assets](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) específica para usuários de criação (depende do nível de assinatura) e por uma limitação de tamanho máximo de arquivo de 5 GB. O espaço também é limitado pela cota de ativos que a organização tem no serviço principal do Adobe Experience Cloud Assets.

* **Requisitos de espaço:** os arquivos nas pastas compartilhadas também devem ser fisicamente armazenados na conta [!DNL Experience Manager] e depois na conta [!DNL Creative Cloud], com uma cópia em cache no serviço principal [!DNL Experience Cloud Assets].
* **Rede e largura de banda:** os arquivos nas pastas compartilhadas e todas as atualizações devem ser transportados pela rede entre os sistemas. Certifique-se de que somente os arquivos e as atualizações relevantes sejam compartilhados.
* **Tipo de pasta**: não há suporte para o compartilhamento de uma pasta [!DNL Assets] do tipo `sling:OrderedFolder` no contexto de compartilhamento em [!DNL Adobe Experience Cloud]. Para compartilhar uma pasta, ao criá-la em [!DNL Assets], não selecione a opção [!UICONTROL Ordenado].

## Práticas recomendadas {#best-practices}

As práticas recomendadas para usar o compartilhamento de pastas do [!DNL Experience Manager] para [!DNL Creative Cloud] incluem:

* **Considerações sobre volume:** [!DNL Experience Manager] e [!DNL Creative Cloud] O Compartilhamento de pastas deve ser usado para compartilhar um número menor de arquivos, por exemplo, relevantes para uma campanha ou atividade específica. Para compartilhar conjuntos maiores de ativos, como todos os ativos aprovados na organização, use outros métodos de distribuição (por exemplo, [!DNL Assets Brand Portal]) ou o aplicativo de desktop [!DNL Experience Manager].
* **Evite compartilhar hierarquias profundas:** O compartilhamento funciona de forma recursiva e não permite o descompartilhamento seletivo. Normalmente, somente as pastas sem subpastas ou com uma hierarquia superficial, como um nível de subpasta, devem ser consideradas para compartilhamento.
* **Pastas separadas para compartilhamento unidirecional:** Pastas separadas devem ser usadas para compartilhar ativos finais de [!DNL Assets] para arquivos [!DNL Creative Cloud] e para compartilhar ativos prontos para criação de volta de [!DNL Creative Cloud] arquivos para [!DNL Assets]. Juntamente com uma boa convenção de nomenclatura para essas pastas, cria um ambiente de trabalho mais fácil de entender para usuários do [!DNL Assets] e do [!DNL Creative Cloud].
* **Evite o WIP na pasta compartilhada:** Não use uma pasta compartilhada para Trabalho em Andamento - use uma pasta separada em Arquivos Creative Cloud para realizar trabalhos que exijam alterações frequentes no arquivo.
* **Iniciar novo trabalho fora da pasta compartilhada:** Os novos designs (arquivos de criação) devem ser iniciados na pasta WIP separada em Arquivos Creative Cloud e, quando estiverem prontos para serem compartilhados com [!DNL Assets] usuários, eles deverão ser movidos ou salvos na pasta compartilhada.
* **Simplifique a estrutura de compartilhamento:** Para uma configuração operacional mais gerenciável, pense em simplificar a estrutura de compartilhamento. Em vez de compartilhar com todos os usuários criativos, as pastas do [!DNL Assets] devem ser compartilhadas somente com representantes da equipe, como um diretor criativo ou gerente de equipe. O gerente do lado criativo receberia os ativos finais, decidiria as atribuições de trabalho e deixaria os designers trabalharem em suas próprias contas do Creative Cloud em ativos do WIP. Eles podem usar os recursos de colaboração em Creative Cloud para coordenar o trabalho e, finalmente, selecionar e colocar os ativos prontos para compartilhamento no [!DNL Assets] em sua pasta compartilhada criativa.

O diagrama a seguir ilustra um exemplo de configuração para criar designs com base nos ativos finais existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)

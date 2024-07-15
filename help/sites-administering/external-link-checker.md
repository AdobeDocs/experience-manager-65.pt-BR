---
title: O Verificador de links
description: O Verificador de links ajuda a validar links internos e externos e permite a regravação de links.
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# O Verificador de links {#the-link-checker}

Os autores de conteúdo não devem se preocupar em validar cada link incluído em suas páginas de conteúdo.

O Verificador de links é executado automaticamente para ajudar os autores de conteúdo com seus links, incluindo:

* Validação de links conforme são adicionados ao conteúdo
* Exibição de uma lista de todos os links externos no conteúdo
* Execução de transformações de links

O Verificador de Links tem várias [opções de configuração](#configuring), como definir a validação interna, permitir que determinados links ou padrões de links sejam omitidos da validação e regravar regras de regravação de links.

O Verificador de links valida [links internos](#internal) e [links externos.](#external)

>[!NOTE]
>
>Como o Verificador de links verifica os links de cada página de conteúdo, o Verificador de links pode afetar o desempenho em repositórios grandes. Nesses casos, talvez seja necessário [configurar com que frequência o Verificador de Links é executado](#configuring) ou [desabilitá-lo.](#disabling)

## Verificação interna de links {#internal}

Links internos são links para outro conteúdo no repositório AEM. Links internos podem ser adicionados usando o seletor de caminho do RTE ou usando um componente personalizado. Por exemplo:

* Sua página `/content/wknd/us/en/adventures/ski-touring.html`
* Contém um link para `/content/wknd/us/en/adventures/extreme-ironing.html` em um componente de Texto [.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Os links internos são validados assim que o autor de conteúdo adiciona um link interno a uma página. Se o link se tornar inválido:

* Ele foi removido do editor. O texto do link permanece, mas o próprio link é removido.
* É mostrado como um link quebrado na interface de criação do.

![Link interno corrompido ao criar uma página](assets/link-checker-invalid-link-internal.png)

## Verificação de links externos {#external}

Links externos são links para conteúdo fora do repositório AEM. Links externos podem ser adicionados usando o RTE ou usando um componente personalizado. Por exemplo:

* Sua página `/content/wknd/us/en/adventures/ski-touring.html`
* Contém um link para `https://bunwarmerthermalunderwear.com` em um componente de Texto [.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Os links externos são validados para sintaxe e por meio da verificação de sua disponibilidade. Essa verificação é feita de forma assíncrona em um local interno configurável. Se o Verificador de links encontrar um link externo inválido:

* Ele foi removido do editor. O texto do link permanece, mas o próprio link é removido.
* É mostrado como um link quebrado na interface de criação do.

![Link interno corrompido ao criar uma página](assets/link-checker-invalid-link-external.png)

Além disso, a interface do [Verificador de links externos](#external-link-checker) fornece uma visão geral de todos os links externos nas suas páginas de conteúdo.

### Utilização do Verificador de links externos {#external-link-checker}

Para usar o Verificador de links externos:

1. Usando a **Navegação**, selecione **Ferramentas** e depois **Sites**.
1. Selecione **Verificador de Links Externos** e uma lista de todos os links externos será exibida.

![A janela do Verificador de Links Externos](assets/external-link-checker.png)

As seguintes informações são exibidas:

* **Status** - O status de validação do link que pode ser um dos seguintes:
   * **Válido** - O link externo pode ser acessado pelo Verificador de Links
   * **Pendente** - O link externo foi adicionado ao conteúdo do site, mas ainda não foi validado pelo Verificador de Links
   * **Inválido** - O link externo não pode ser acessado pelo Verificador de Links
* **URL** - O link externo
* **Referenciador** - A página de conteúdo que contém o link externo
   * Isto é populado somente [se configurado.](#configuring)
* **Última Verificação** - A última vez que o Verificador de Links validou o link externo
   * A frequência com que os links são verificados [é configurável.](#configuring)
* **Último status** - O último código de status de HTML retornado quando o link foi verificado pela última vez no link externo
* **Último disponível** - Tempo desde que o link ficou disponível pela última vez para o Verificador de links
* **Último acesso** - tempo desde que a página com o link externo foi acessada pela última vez na interface de criação

É possível manipular o conteúdo da janela usando os dois botões na parte superior da lista de links:

* **Atualizar** - Para atualizar o conteúdo da lista
* **Verificar** - Para verificar um link externo individual selecionado na lista

### Como funciona o Verificador de links externos {#how-it-works}

Embora fácil de usar, o Verificador de links externos depende de vários serviços e entender como eles funcionam ajuda você a entender como [configurar o Verificador de links](#configuring) para atender às suas necessidades.

1. Sempre que um autor de conteúdo salva qualquer link para uma página, um manipulador de eventos é acionado.
1. O manipulador de eventos percorre todo o conteúdo em `/content`, verifica se há links novos ou atualizados e os adiciona a um cache para o Verificador de links.
1. O **Serviço Verificador de Links CQ do Dia** é executado em um agendamento regular para verificar se as entradas no cache têm sintaxe válida.
1. Os links validados por sintaxe aparecem na janela [Verificador de links externos](#external-link-checker). No entanto, eles estarão em um estado **Pendente**.
1. A **Tarefa do Verificador de Links do CQ de Dias** é executada regularmente para validar os links fazendo uma chamada GET.
1. A **Tarefa do Verificador de Links CQ do Dia** atualiza as entradas na janela Verificador de Links Externos com os resultados das chamadas de GET.

## Configuração do Verificador de links {#configuring}

O Verificador de links está disponível automaticamente e pronto para uso no AEM. No entanto, há várias configurações de OSGi que podem ser modificadas para alterar seu comportamento:

* **Serviço de Armazenamento de Informações do Verificador de Links CQ do Dia** - Esse serviço define o tamanho do cache do Verificador de Links no repositório.
* **Serviço Day CQ Verificador de Links** - Esse serviço executa a verificação assíncrona da sintaxe de links externos. Você pode definir o período de verificação e quais tipos de links são ignorados pelo verificador entre outras opções.
* **Tarefa do Verificador de Links CQ de Dias** - Esse serviço executa a validação de links externos para GET. Ela permite definições separadas de intervalos para verificar links ruins e bons entre outras opções.
* **Transformador do Verificador de Links CQ de Dias** - Permite converter links com base em um conjunto de regras definido pelo usuário.

Consulte o documento [Configurações de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obter mais detalhes sobre como alterar configurações de OSGi.

## Desativar o Verificador de links {#disabling}

Você pode optar por desativar totalmente o Verificador de links. Para fazer isso:

1. Abra o console OSGi.
1. Editar o **Transformador do Verificador de links CQ de dias**
1. Marque as opções que deseja desativar:
   * **Desabilitar Verificação** - para desabilitar a validação de links
   * **Desabilitar Regravação** - para desabilitar transformações de link

>[!NOTE]
>
>Se você desabilitar a verificação de links depois de começar a criar o conteúdo, ainda poderá ver entradas na [janela Verificador de Links Externos](#external-link-checker), mas elas não serão mais atualizadas.

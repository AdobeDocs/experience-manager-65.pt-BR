---
title: O Verificador de links
description: O Verificador de links ajuda a validar links internos e externos e permite a regravação de links.
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 0%

---

# O Verificador de links {#the-link-checker}

Os autores de conteúdo não devem se preocupar em validar cada link incluído em suas páginas de conteúdo.

O Verificador de links é executado automaticamente para ajudar os autores de conteúdo com seus links, incluindo:

* Validação de links conforme são adicionados ao conteúdo
* Exibição de uma lista de todos os links externos no conteúdo
* Execução de transformações de links

O Verificador de links tem vários [opções de configuração](#configuring) como definir a validação interna, permitir que determinados links ou padrões de links sejam omitidos da validação e reescrever regras de reescrita de links.

O Verificador de links valida ambos [links internos](#internal) e [links externos.](#external)

>[!NOTE]
>
>Como o Verificador de links verifica os links de cada página de conteúdo, o Verificador de links pode afetar o desempenho em repositórios grandes. Nesses casos, talvez seja necessário [configurar a frequência com que o Verificador de links é executado](#configuring) ou [desative-o.](#disabling)

## Verificação interna de links {#internal}

Links internos são links para outro conteúdo no repositório AEM. Links internos podem ser adicionados usando o seletor de caminho do RTE ou usando um componente personalizado. Por exemplo:

* Sua página `/content/wknd/us/en/adventures/ski-touring.html`
* Conter um link para `/content/wknd/us/en/adventures/extreme-ironing.html` em um [Componente de Texto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Os links internos são validados assim que o autor de conteúdo adiciona um link interno a uma página. Se o link se tornar inválido:

* Ele foi removido do editor. O texto do link permanece, mas o próprio link é removido.
* É mostrado como um link quebrado na interface de criação do.

![Link interno corrompido ao criar uma página](assets/link-checker-invalid-link-internal.png)

## Verificação de links externos {#external}

Links externos são links para conteúdo fora do repositório AEM. Links externos podem ser adicionados usando o RTE ou usando um componente personalizado. Por exemplo:

* Sua página `/content/wknd/us/en/adventures/ski-touring.html`
* Conter um link para `https://bunwarmerthermalunderwear.com` em um [Componente de Texto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Os links externos são validados para sintaxe e por meio da verificação de sua disponibilidade. Essa verificação é feita de forma assíncrona em um local interno configurável. Se o Verificador de links encontrar um link externo inválido:

* Ele foi removido do editor. O texto do link permanece, mas o próprio link é removido.
* É mostrado como um link quebrado na interface de criação do.

![Link interno corrompido ao criar uma página](assets/link-checker-invalid-link-external.png)

Além disso, a [Verificador de links externos](#external-link-checker) A interface do fornece uma visão geral de todos os links externos nas páginas de conteúdo.

### Utilização do Verificador de links externos {#external-link-checker}

Para usar o Verificador de links externos:

1. Usar **Navegação**, selecione **Ferramentas**, depois **Sites**.
1. Selecionar **Verificador de links externos** e uma lista de todos os links externos é exibida.

![A janela Verificador de links externos](assets/external-link-checker.png)

As seguintes informações são exibidas:

* **Status** - O status de validação do link, que pode ser um dos seguintes:
   * **Válido** - O link externo pode ser acessado pelo Verificador de links
   * **Pending** - O link externo foi adicionado ao conteúdo do site, mas ainda não foi validado pelo Verificador de links
   * **Inválido** - O link externo não pode ser acessado pelo Verificador de links
* **URL** - Quanto ao vínculo externo
* **Referenciador** - A página de conteúdo que contém o link externo
   * Isto é apenas preenchido [se configurado.](#configuring)
* **Última verificação** - A última vez que o Verificador de links validou o link externo
   * Com que frequência os links são verificados [é configurável.](#configuring)
* **Último status** - O último código de status de HTML retornado quando o link foi verificado pela última vez no link externo
* **Último disponível** - Tempo desde que o link ficou disponível pela última vez para o Verificador de links
* **Acessado por última vez** - tempo desde que a página com o link externo foi acessada pela última vez na interface de criação

É possível manipular o conteúdo da janela usando os dois botões na parte superior da lista de links:

* **Atualizar** - Para atualizar o conteúdo da lista
* **Marcar** - Para verificar um link externo individual selecionado na lista

### Como funciona o Verificador de links externos {#how-it-works}

Embora fácil de usar, o Verificador de links externos depende de vários serviços e entender como eles funcionam ajuda a entender como [configurar o Verificador de links](#configuring) para atender às suas necessidades.

1. Sempre que um autor de conteúdo salva qualquer link para uma página, um manipulador de eventos é acionado.
1. O manipulador de eventos percorre todo o conteúdo em `/content` O e o verificam links novos ou atualizados e os adicionam a um cache do Verificador de links.
1. A variável **Serviço Day CQ Verificador de links** O então é executado regularmente para verificar se as entradas no cache têm sintaxe válida.
1. Os links validados pela sintaxe aparecem na variável [Verificador de links externos](#external-link-checker) janela. No entanto, eles estarão em uma **Pending** estado.
1. A variável **Tarefa do Verificador de Links CQ Diário** em seguida, o é executado regularmente para validar os links, fazendo uma chamada GET.
1. A variável **Tarefa do Verificador de Links CQ Diário** Em seguida, o atualiza as entradas na janela Verificador de links externos com os resultados das chamadas do GET.

## Configuração do Verificador de links {#configuring}

O Verificador de links está disponível automaticamente e pronto para uso no AEM. No entanto, há várias configurações de OSGi que podem ser modificadas para alterar seu comportamento:

* **Serviço de armazenamento de informações do verificador de links CQ diário** - Este serviço define o tamanho do cache do Verificador de links no repositório.
* **Serviço Day CQ Verificador de links** - Esse serviço executa a verificação assíncrona da sintaxe de links externos. Você pode definir o período de verificação e quais tipos de links são ignorados pelo verificador entre outras opções.
* **Tarefa do Verificador de Links CQ Diário** - Este serviço executa a validação de GET de links externos. Ela permite definições separadas de intervalos para verificar links ruins e bons entre outras opções.
* **Transformador do Verificador de links CQ diário** - Permite converter links com base em um conjunto de regras definido pelo usuário.

Consulte o documento [Configurações do OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obter mais detalhes sobre como alterar configurações de OSGi.

## Desativar o Verificador de links {#disabling}

Você pode optar por desativar totalmente o Verificador de links. Para fazer isso:

1. Abra o console OSGi.
1. Edite o **Transformador do Verificador de links CQ diário**
1. Marque as opções que deseja desativar:
   * **Desativar verificação** - para desativar a validação de links
   * **Desativar regravação** - para desativar transformações de links

>[!NOTE]
>
>Se você desativar a verificação de links depois de começar a criar o conteúdo, ainda poderá ver entradas no [Janela Verificador de links externos](#external-link-checker), mas não serão mais atualizados.

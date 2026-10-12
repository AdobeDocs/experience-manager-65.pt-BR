---
title: Prevenção de ataques CSRF
description: Saiba como impedir ataques de falsificação de solicitação entre sites (CSRF) e proteger os dados do usuário de serem comprometidos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%
---
# Prevenção de ataques CSRF {#preventing-csrf-attacks}

## Como os ataques de CSRF funcionam {#how-csrf-attacks-work}

A falsificação de solicitação entre sites (CSRF) é uma vulnerabilidade de site em que o navegador de um usuário válido é usado para enviar uma solicitação mal-intencionada, possivelmente por meio de um iFrame. Como o navegador envia cookies com base em domínio, se o usuário estiver conectado a um aplicativo, os dados do usuário podem ficar comprometidos.

Por exemplo, considere um cenário em que você esteja conectado ao console de administração em um navegador. Você recebe uma mensagem de email contendo um link. Você clica no link, que abre uma nova guia no navegador. A página aberta contém um iFrame oculto que faz uma solicitação mal-intencionada ao servidor do Forms usando o cookie da sessão autenticada do AEM Forms. Como o Gerenciamento de usuários recebe um cookie válido, ele transmite a solicitação.

## Termos relacionados ao CSRF {#csrf-related-terms}

**Referenciador:** O endereço da página de origem da qual uma solicitação está vindo. Por exemplo, uma página da Web em site1.com contém um link para site2.com. Clicar no link publica uma solicitação em site2.com. O referenciador desta solicitação é site1.com porque a solicitação é feita de uma página cuja origem é site1.com.

**URIs minuciados:** URIs identificam recursos no Forms Server que estão sendo solicitados, por exemplo, /adi ou /contentspace. Alguns recursos podem permitir que uma solicitação entre no aplicativo a partir de sites externos. Esses recursos são considerados URIs classificados. O Forms Server nunca executa uma verificação de referenciador a partir de URIs.

**Referenciador nulo:** Quando você abre uma nova janela ou guia do navegador, digita um endereço e pressiona Enter, o referenciador é nulo. A solicitação é totalmente nova e não se origina de uma página da Web pai; portanto, não há referenciador para a solicitação. O servidor do Forms pode receber um referenciador nulo de:

* solicitações feitas em endpoints SOAP ou REST do Acrobat
* qualquer cliente de desktop que faça uma solicitação HTTP em um terminal AEM forms SOAP ou REST
* quando uma nova janela do navegador é aberta e o URL de qualquer página de logon de aplicativo web do AEM forms é inserido

Permitir um referenciador nulo em pontos de extremidade SOAP e REST. Também permite um referenciador nulo em todas as páginas de logon do URI, como /adminui e /contentspace, e seus recursos mapeados correspondentes. Por exemplo, o servlet mapeado para /contentspace é /contentspace/faces/jsp/login.jsp, que deve ser uma exceção de referenciador nulo. Essa exceção é necessária somente se você habilitar a filtragem GET para o aplicativo web. Seus aplicativos podem especificar se devem permitir referenciadores nulos. Consulte &quot;Proteção contra ataques de falsificação de solicitação entre sites&quot; em [Proteção e segurança para o AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Exceção de Referenciador Permitida:** Exceção de Referenciador Permitida é uma sublista da lista de referenciadores permitidos, da qual as solicitações são bloqueadas. Permitido As exceções de referência são específicas a um aplicativo web. Se um subconjunto de Referenciadores permitidos não tiver permissão para chamar uma aplicação Web específica, você poderá incluir na lista de bloqueios os referenciadores por meio de Exceções de referenciador permitidas. As Exceções de referenciador permitidas são especificadas no arquivo web.xml do aplicativo. (Consulte &quot;Protegendo contra ataques de falsificação de solicitação entre sites&quot; em Fortalecimento e segurança para formulários do AEM na página Ajuda e tutoriais.)

## Como os referenciadores permitidos funcionam {#how-allowed-referers-work}

O AEM Forms fornece filtragem de referenciador, que pode ajudar a impedir ataques CSRF. Veja como a filtragem de referenciador funciona:

1. O Forms Server verifica o método HTTP usado para invocação:

   * Se for POST, o Forms Server executará a verificação do cabeçalho do referenciador.
   * Se for GET, o Forms Server ignorará a verificação do referenciador, a menos que CSRF_CHECK_GETS esteja definido como true, nesse caso, ele executa a verificação do cabeçalho do referenciador. CSRF_CHECK_GETS é especificado no arquivo web.xml do aplicativo. (Consulte &quot;Protegendo contra ataques de falsificação de solicitação entre sites&quot; no [Guia de Proteção e Segurança](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. O servidor do Forms verifica se o URI solicitado é:

   * Se o URI for atualizado, o servidor transmitirá a solicitação.
   * Se o URI solicitado não for reconhecido, o servidor recuperará o referenciador da solicitação.

1. Se houver um referenciador na solicitação, o servidor verificará se ele é um referenciador permitido. Se for permitido, o servidor verificará se há uma exceção do referenciador:

   * Se for uma exceção, a solicitação será bloqueada.
   * Se não for uma exceção, a solicitação será transmitida.

1. Se não houver referenciador na solicitação, o servidor verificará se um referenciador nulo é permitido.

   * Se um referenciador nulo for permitido, a solicitação será transmitida.
   * Se um referenciador nulo não for permitido, o servidor verificará se o URI solicitado é uma exceção para referenciador nulo e lidará com a solicitação adequadamente.

## Configurar referenciadores permitidos {#configure-allowed-referers}

Quando você executa o Configuration Manager, o host padrão e o endereço IP do Forms Server são adicionados à lista Referenciador permitido. Você pode editar essa lista no console de administração.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar URLs de referenciador permitidos. A lista Referenciador permitido é exibida na parte inferior da página.
1. Para adicionar um referenciador permitido:

   * Digite um nome de host ou endereço IP na caixa Referenciadores permitidos. Para adicionar mais de um referenciador permitido por vez, digite cada nome de host ou endereço IP em uma nova linha.
   * Nas caixas Porta HTTP e Portas HTTPS, especifique quais portas permitir para HTTP, HTTPS ou ambos. Se essas caixas estiverem vazias, as portas padrão (porta 80 para HTTP e porta 443 para HTTPS) serão usadas. Se você digitar `0` (zero) nas caixas, todas as portas nesse servidor serão habilitadas. Você também pode inserir um número de porta específico para habilitar somente essa porta.
   * Clique em Adicionar.

1. Para remover a entrada da lista Referenciador permitido, selecione o item na lista e clique em Excluir.

   Se a Lista de referenciadores permitidos estiver vazia, o recurso CSRF para de funcionar e o sistema fica inseguro.

1. Depois de alterar a lista de Referenciadores permitidos, reinicie o AEM Forms Server.

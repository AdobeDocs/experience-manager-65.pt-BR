---
title: Prevenção de ataques CSRF
seo-title: Preventing CSRF attacks
description: Saiba como impedir ataques de falsificação de solicitação entre sites (CSRF) e proteger os dados do usuário de serem comprometidos.
seo-description: Learn how to prevent Cross-site request forgery (CSRF) attacks and safeguard user data from being compromised.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# Prevenção de ataques CSRF {#preventing-csrf-attacks}

## Como os ataques de CSRF funcionam {#how-csrf-attacks-work}

A falsificação de solicitação entre sites (CSRF) é uma vulnerabilidade de site em que o navegador de um usuário válido é usado para enviar uma solicitação mal-intencionada, possivelmente por meio de um iFrame. Como o navegador envia cookies com base em domínio, se o usuário estiver conectado no momento a um aplicativo, os dados do usuário podem ficar comprometidos.

Por exemplo, considere um cenário em que você esteja conectado ao console de administração em um navegador. Você recebe uma mensagem de email contendo um link. Você clica no link, que abre uma nova guia no navegador. A página que você abriu contém um iFrame oculto que faz uma solicitação mal-intencionada ao servidor de formulários usando o cookie da sua sessão autenticada do AEM Forms. Como o Gerenciamento de usuários recebe um cookie válido, ele transmite a solicitação.

## Termos relacionados ao CSRF {#csrf-related-terms}

**Referenciador:** O endereço da página de origem da qual uma solicitação é recebida. Por exemplo, uma página da Web em site1.com contém um link para site2.com. Clicar no link publica uma solicitação em site2.com. O referenciador dessa solicitação é site1.com porque a solicitação é feita de uma página cuja origem é site1.com.

**Incluir na lista de permissões URIs resolvidas:** Os URIs identificam recursos no servidor de formulários que estão sendo solicitados, por exemplo, /adminui ou /contentspace. Alguns recursos podem permitir que uma solicitação entre no aplicativo a partir de sites externos. Incluir na lista de permissões Esses recursos são considerados URIs classificados. Incluir na lista de permissões O servidor do Forms nunca executa uma verificação de referenciador a partir de URIs resolvidos.

**Referenciador nulo:** Ao abrir uma nova janela ou guia do navegador, digitar um endereço e pressionar Enter, o referenciador é nulo. A solicitação é totalmente nova e não se origina de uma página da Web pai; portanto, não há referenciador para a solicitação. O servidor de formulários pode receber uma referência nula de:

* solicitações feitas em endpoints SOAP ou REST do Acrobat
* qualquer cliente de desktop que faça uma solicitação HTTP em um ponto de extremidade AEM forma SOAP ou REST
* quando uma nova janela do navegador é aberta e o URL de qualquer página de logon de aplicativo web AEM forms é inserido

Permitir uma referência nula em pontos de extremidade SOAP e REST. Também permita um referenciador nulo em todas as páginas de logon de URI, como /adminui e /contentspace e seus recursos mapeados correspondentes. Por exemplo, o servlet mapeado para /contentspace é /contentspace/faces/jsp/login.jsp, que deve ser uma exceção de referenciador nulo. Essa exceção é necessária somente se você habilitar a filtragem de GET para seu aplicativo web. Seus aplicativos podem especificar se devem permitir referenciadores nulos. Consulte &quot;Protegendo contra ataques de falsificação de solicitação entre sites&quot; em [Fortalecimento e segurança para formulários AEM](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Exceção de referenciador permitida:** Exceção de referenciador permitida é uma sublista da lista de referenciadores permitidos, da qual as solicitações são bloqueadas. Permitido As exceções de referência são específicas a um aplicativo web. Se um subconjunto de Referenciadores permitidos não tiver permissão para chamar uma aplicação Web específica, você poderá incluir na lista de bloqueios os referenciadores por meio das Exceções de referenciador permitidas. As Exceções de referenciador permitidas são especificadas no arquivo web.xml do aplicativo. (Consulte &quot;Protegendo contra ataques de falsificação de solicitação entre sites&quot; em Fortalecimento e segurança para formulários AEM na página Ajuda e Tutorials.)

## Como os referenciadores permitidos funcionam {#how-allowed-referers-work}

Os formulários AEM fornecem filtragem de referência, que pode ajudar a impedir ataques CSRF. Veja como a filtragem de referência funciona:

1. O servidor de formulários verifica o método HTTP usado para invocação:

   * Se for POST, o servidor de formulários executará a verificação do cabeçalho de referência.
   * Se for GET, o servidor de formulários ignorará a verificação de referenciador, a menos que CSRF_CHECK_GETS esteja definido como verdadeiro, nesse caso, ele executará a verificação de cabeçalho de referenciador. CSRF_CHECK_GETS é especificado no arquivo web.xml do aplicativo. (Consulte &quot;Protegendo contra ataques de falsificação de solicitação entre sites&quot; em [Guia de proteção e segurança](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. Incluir na lista de permissões O servidor de formulários verifica se o URI solicitado é:

   * Incluir na lista de permissões Se o URI for atualizado, o servidor transmitirá a solicitação.
   * Incluir na lista de permissões Se o URI solicitado não for reconhecido, o servidor recuperará o referenciador da solicitação.

1. Se houver um referenciador na solicitação, o servidor verificará se ele é um referenciador permitido. Se for permitido, o servidor verificará se há uma exceção de referenciador:

   * Se for uma exceção, a solicitação será bloqueada.
   * Se não for uma exceção, a solicitação será transmitida.

1. Se não houver referenciador na solicitação, o servidor verificará se um referenciador nulo é permitido.

   * Se um referenciador nulo for permitido, a solicitação será transmitida.
   * Se um referenciador nulo não for permitido, o servidor verificará se o URI solicitado é uma exceção para referenciador nulo e manipulará a solicitação adequadamente.

## Configurar referenciadores permitidos {#configure-allowed-referers}

Quando você executa o Configuration Manager, o host padrão e o endereço IP ou o servidor de formulários são adicionados à lista Referenciador permitido. Você pode editar essa lista no console de administração.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar URLs de referência permitidos. A lista Referenciador permitido é exibida na parte inferior da página.
1. Para adicionar um referenciador permitido:

   * Digite um nome de host ou endereço IP na caixa Referenciadores permitidos. Para adicionar mais de um referenciador permitido por vez, digite cada nome de host ou endereço IP em uma nova linha.
   * Nas caixas Porta HTTP e Portas HTTPS, especifique quais portas permitir para HTTP, HTTPS ou ambos. Se essas caixas estiverem vazias, as portas padrão (porta 80 para HTTP e porta 443 para HTTPS) serão usadas. Se você inserir `0` (zero) nas caixas, todas as portas nesse servidor são ativadas. Você também pode inserir um número de porta específico para habilitar somente essa porta.
   * Clique em Adicionar.

1. Para remover a entrada da lista Referenciador permitido, selecione o item na lista e clique em Excluir.

   Se a Lista de referenciadores permitidos estiver vazia, o recurso CSRF para de funcionar e o sistema fica inseguro.

1. Depois de alterar a lista de Referenciadores permitidos, reinicie o servidor de formulários AEM.

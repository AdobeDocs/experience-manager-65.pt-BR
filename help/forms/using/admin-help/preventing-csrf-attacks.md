---
title: Evitando ataques de CSRF
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

# Evitando ataques de CSRF {#preventing-csrf-attacks}

## Como funcionam os ataques de CSRF {#how-csrf-attacks-work}

A falsificação de solicitação entre sites (CSRF) é uma vulnerabilidade de site, onde um navegador de usuário válido é usado para enviar uma solicitação mal-intencionada, possivelmente por meio de um iFrame. Como o navegador envia cookies por domínio, se o usuário estiver conectado no momento a um aplicativo, os dados do usuário podem estar comprometidos.

Por exemplo, considere um cenário em que você está conectado ao console de administração em um navegador. Você recebe uma mensagem de email contendo um link. Você clica no link , o que abre uma nova guia no navegador. A página que você abriu contém um iFrame oculto que faz uma solicitação mal-intencionada ao servidor de formulários usando o cookie da sessão de formulários de AEM autenticados. Como o Gerenciamento de usuários recebe um cookie válido, ele transmite a solicitação.

## Termos relacionados ao CSRF {#csrf-related-terms}

**Referenciador:** O endereço da página de origem da qual uma solicitação está vindo. Por exemplo, uma página da Web em site1.com contém um link para site2.com. Clicar no link publica uma solicitação para site2.com. O referenciador desta solicitação é site1.com porque a solicitação é feita de uma página cuja fonte é site1.com.

**URIs Incluir na lista de permissões:** Os URIs identificam recursos no servidor de formulários que estão sendo solicitados, por exemplo, /adminui ou /contentspace. Alguns recursos podem permitir que uma solicitação insira o aplicativo de sites externos. Esses recursos são considerados URIs incluir na lista de permissões. O servidor de formulários nunca executa uma verificação de referenciador de URIs incluir na lista de permissões.

**Referenciador nulo:** Ao abrir uma nova janela ou guia do navegador, digite um endereço e pressione Enter, o referenciador é nulo. A solicitação é totalmente nova e não tem origem em uma página da Web principal; portanto, não há referenciador para a solicitação. O servidor de formulários pode receber um referenciador nulo de:

* solicitações feitas em endpoints SOAP ou REST do Acrobat
* qualquer cliente de desktop que faça uma solicitação HTTP em um ponto de extremidade AEM SOAP ou REST dos formulários
* quando uma nova janela do navegador é aberta e o URL para qualquer página de logon de aplicativo da web de formulários AEM é inserido

Permita um referenciador nulo em pontos de extremidade SOAP e REST. Permita também um referenciador nulo em todas as páginas de logon do URI, como /adminui e /contentspace, e seus recursos mapeados correspondentes. Por exemplo, o servlet mapeado para /contentspace é /contentspace/faces/jsp/login.jsp, que deve ser uma exceção de referenciador nula. Essa exceção é necessária somente se você habilitar a filtragem de GET para sua aplicação Web. Seus aplicativos podem especificar se permitem referenciadores nulos. Consulte &quot;Protegendo contra ataques de falsificação de solicitações entre sites&quot; em [Otimização e segurança para formulários AEM](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Exceção de Referenciador Permitida:** Exceção de referenciador permitida é uma sublista da lista de referenciadores permitidos, a partir da qual as solicitações são bloqueadas. As Exceções de Referência Permitidas são específicas de um aplicativo Web. Se um subconjunto dos Referenciadores permitidos não tiver permissão para invocar um determinado aplicativo Web, você poderá lista de bloqueios os referenciadores por meio de Exceções de Referenciador Permitidas. As Exceções de Referenciador Permitidas são especificadas no arquivo web.xml para seu aplicativo. (Consulte &quot;Proteção contra ataques de falsificação de solicitações entre sites&quot; em Proteção e segurança para formulários AEM na página Ajuda e Tutorials.)

## Como os referenciadores permitidos funcionam {#how-allowed-referers-work}

AEM formulários fornece filtragem de referenciador, o que pode ajudar a impedir ataques de CSRF. Veja como a filtragem de referenciador funciona:

1. O servidor de formulários verifica o método HTTP usado para invocação:

   * Se for POST, o servidor de formulários executará a verificação do cabeçalho do referenciador.
   * Se for GET, o servidor de formulários ignora a verificação do referenciador, a menos que CSRF_CHECK_GETS esteja definido como true, nesse caso, ele executa a verificação do cabeçalho do referenciador. CSRF_CHECK_GETS é especificado no arquivo web.xml para seu aplicativo. (Consulte &quot;Protegendo contra ataques de falsificação de solicitações entre sites&quot; em [Guia de proteção e segurança](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. O servidor de formulários verifica se o URI solicitado está incluir na lista de permissões:

   * Se o URI for incluir na lista de permissões, o servidor passará a solicitação.
   * Se o URI solicitado não for incluir na lista de permissões, o servidor recuperará o referenciador da solicitação.

1. Se houver um referenciador na solicitação, o servidor verificará se é um referenciador permitido. Se for permitido, o servidor verifica se há uma exceção de referenciador:

   * Se for uma exceção, a solicitação será bloqueada.
   * Se não for uma exceção, a solicitação será passada.

1. Se não houver referenciador na solicitação, o servidor verificará se um referenciador nulo é permitido.

   * Se um referenciador nulo for permitido, a solicitação será passada.
   * Se um referenciador nulo não for permitido, o servidor verificará se o URI solicitado é uma exceção para referenciador nulo e manipulará a solicitação de acordo.

## Configurar referenciadores permitidos {#configure-allowed-referers}

Ao executar o Configuration Manager, o host padrão e o endereço IP ou o servidor de formulários são adicionados à lista Referenciador permitido. É possível editar essa lista no console de administração.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar URLs de referenciador permitidos. A lista Referenciador permitido é exibida na parte inferior da página.
1. Para adicionar um referenciador permitido:

   * Digite um nome de host ou endereço IP na caixa Referenciadores permitidos . Para adicionar mais de um referenciador permitido de cada vez, digite cada nome de host ou endereço IP em uma nova linha.
   * Nas caixas Porta HTTP e Portas HTTPS, especifique quais portas devem permitir HTTP, HTTPS ou ambos. Se deixar essas caixas vazias, as portas padrão (porta 80 para HTTP e porta 443 para HTTPS) serão usadas. Se você inserir `0` (zero) nas caixas, todas as portas desse servidor são ativadas. Você também pode inserir um número de porta específico para habilitar somente essa porta.
   * Clique em Adicionar.

1. Para remover a entrada da lista Referenciador Permitido, selecione o item na lista e clique em Excluir.

   Se a Lista de referenciadores permitidos estiver vazia, o recurso CSRF parará de funcionar e o sistema ficará inseguro.

1. Depois de alterar a lista Referenciador permitido, reinicie o servidor de formulários AEM.

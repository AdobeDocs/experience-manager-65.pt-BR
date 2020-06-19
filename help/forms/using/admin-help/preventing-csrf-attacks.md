---
title: Prevenção de ataques CSRF
seo-title: Prevenção de ataques CSRF
description: Saiba como impedir ataques de falsificação de solicitação entre sites (CSRF) e proteger os dados do usuário de serem comprometidos.
seo-description: Saiba como impedir ataques de falsificação de solicitação entre sites (CSRF) e proteger os dados do usuário de serem comprometidos.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# Prevenção de ataques CSRF {#preventing-csrf-attacks}

## Como funcionam os ataques de CSRF {#how-csrf-attacks-work}

A falsificação de solicitação entre sites (CSRF) é uma vulnerabilidade de site na qual um navegador de usuário válido é usado para enviar uma solicitação mal-intencionada, possivelmente por meio de um iFrame. Como o navegador envia cookies por domínio, se o usuário estiver conectado no momento a um aplicativo, os dados do usuário podem estar comprometidos.

Por exemplo, considere um cenário em que você está conectado ao console de administração em um navegador. Você recebe uma mensagem de email contendo um link. Clique no link, que abre uma nova guia no navegador. A página aberta contém um iFrame oculto que faz uma solicitação mal-intencionada ao servidor de formulários usando o cookie da sessão de formulários AEM autenticados. Como o Gerenciamento de usuários recebe um cookie válido, ele envia a solicitação.

## Termos relacionados ao CSRF {#csrf-related-terms}

**Referenciador:** O endereço da página de origem da qual uma solicitação está vindo. Por exemplo, uma página da Web no site1.com contém um link para site2.com. Clicar no link postou uma solicitação para site2.com. O referenciador desta solicitação é site1.com porque a solicitação é feita de uma página cuja fonte é site1.com.

**URIs permitidos:** Os URIs identificam recursos no servidor de formulários que estão sendo solicitados, por exemplo, /adminui ou /contentspace. Alguns recursos podem permitir que uma solicitação entre no aplicativo de sites externos. Esses recursos são considerados URIs permitidos. O servidor de formulários nunca realiza uma verificação de referenciador de URIs permitidos.

**Referenciador nulo:** Quando você abre uma nova janela ou guia do navegador, digite um endereço e pressione Enter, o referenciador é nulo. O pedido é inteiramente novo e não tem origem numa página Web principal; por conseguinte, não existe um referenciador para o pedido. O servidor de formulários pode receber um referenciador nulo de:

* solicitações feitas em pontos de extremidade SOAP ou REST do Acrobat
* qualquer cliente desktop que faça uma solicitação HTTP em um ponto de extremidade SOAP ou REST de formulários AEM
* quando uma nova janela do navegador é aberta e o URL de qualquer página de logon de aplicativo da Web de formulários AEM é inserido

Permita um referenciador nulo nos pontos finais SOAP e REST. Também permite um referenciador nulo em todas as páginas de logon de URI, como /adminui e /contentspace, e seus recursos mapeados correspondentes. Por exemplo, o servlet mapeado para /contentspace é /contentspace/faces/jsp/login.jsp, que deve ser uma exceção de referenciador nula. Essa exceção é necessária somente se você ativar a filtragem GET para seu aplicativo da Web. Seus aplicativos podem especificar se permitem referenciadores nulos. Consulte &quot;Protegendo contra ataques de falsificação de solicitação entre sites&quot; em [Proteção e segurança para formulários](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)AEM.

**Exceção de referenciador permitida:** A Exceção de Referenciador Permitida é uma sublista da lista de referenciadores permitidos, a partir da qual as solicitações são bloqueadas. As Exceções de referência permitidas são específicas a um aplicativo da Web. Se um subconjunto dos Referenciadores permitidos não tiver permissão para invocar um determinado aplicativo da Web, você poderá bloquear a lista de referenciadores por meio de Exceções de referenciador permitidas. Exceções de referenciador permitidas são especificadas no arquivo web.xml para seu aplicativo. (Consulte &quot;Protegendo contra ataques de falsificação de solicitação entre sites&quot; em Formulários de proteção e segurança para AEM na página Ajuda e tutoriais.)

## Como os referenciadores permitidos funcionam {#how-allowed-referers-work}

Os formulários AEM fornecem filtragem de referenciador, o que pode ajudar a impedir ataques CSRF. Veja como a filtragem de referenciador funciona:

1. O servidor de formulários verifica o método HTTP usado para a invocação:

   * Se for POST, o servidor de formulários executará a verificação do cabeçalho do referenciador.
   * Se for GET, o servidor de formulários ignorará a verificação do referenciador, a menos que CSRF_CHECK_GETS esteja definido como true, caso em que executa a verificação do cabeçalho do referenciador. CSRF_CHECK_GETS é especificado no arquivo web.xml para seu aplicativo. (Consulte &quot;Protegendo contra ataques de falsificação de solicitações entre sites&quot; no guia [de](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)proteção e segurança.)

1. O servidor de formulários verifica se o URI solicitado é permitido:

   * Se o URI for permitido na lista, o servidor transmitirá a solicitação.
   * Se o URI solicitado não for permitido na lista, o servidor recuperará o referenciador da solicitação.

1. Se houver um referenciador na solicitação, o servidor verificará se ele é um referenciador permitido. Se for permitido, o servidor verifica se há uma exceção de referenciador:

   * Se for uma exceção, a solicitação será bloqueada.
   * Se não for uma exceção, a solicitação será transmitida.

1. Se não houver referenciador na solicitação, o servidor verificará se um referenciador nulo é permitido.

   * Se um referenciador nulo for permitido, a solicitação será transmitida.
   * Se um referenciador nulo não for permitido, o servidor verificará se o URI solicitado é uma exceção para referenciador nulo e tratará a solicitação de acordo.

## Configurar referenciadores permitidos {#configure-allowed-referers}

Quando você executa o Configuration Manager, o host padrão e o endereço IP ou o servidor de formulários são adicionados à lista Referenciador Permitido. Você pode editar essa lista no console de administração.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar URLs de referência permitidos. A lista Referenciador Permitido é exibida na parte inferior da página.
1. Para adicionar um referenciador permitido:

   * Digite um nome de host ou endereço IP na caixa Referenciadores permitidos. Para adicionar mais de um referenciador permitido de cada vez, digite cada nome de host ou endereço IP em uma nova linha.
   * Nas caixas Porta HTTP e Portas HTTPS, especifique quais portas serão permitidas para HTTP, HTTPS ou ambos. Se você deixar essas caixas vazias, as portas padrão (porta 80 para HTTP e porta 443 para HTTPS) serão usadas. Se você inserir `0` (zero) nas caixas, todas as portas desse servidor serão ativadas. Você também pode inserir um número de porta específico para ativar somente essa porta.
   * Clique em Adicionar.

1. Para remover a entrada da lista Referenciador Permitido, selecione o item da lista e clique em Excluir.

   Se a Lista de referência permitida estiver vazia, o recurso CSRF para de funcionar e o sistema fica inseguro.

1. Depois de alterar a lista de referência permitida, reinicie o servidor de formulários AEM.


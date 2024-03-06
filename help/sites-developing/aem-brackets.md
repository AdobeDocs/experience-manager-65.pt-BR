---
title: Extensão de Colchetes AEM
description: Saiba como usar a extensão Adobe Experience Manager para Colchetes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Extensão de Colchetes AEM{#aem-brackets-extension}

## Visão geral {#overview}

A extensão AEM Brackets fornece um fluxo de trabalho suave para editar componentes AEM e bibliotecas de clientes e usa o poder do [Colchetes](https://brackets.io/) editor de código, que dá acesso a arquivos e camadas do Photoshop a partir do editor de código. A fácil sincronização fornecida pela extensão (sem a necessidade de Maven ou File Vault) aumenta a eficiência do desenvolvedor e também ajuda desenvolvedores de front-end com conhecimento limitado em AEM a participar de projetos. Essa extensão também fornece suporte para o [Linguagem de modelo HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR), que elimina a complexidade do JSP para tornar o desenvolvimento de componentes mais fácil e seguro.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Recursos {#features}

As principais características da extensão de colchetes AEM são:

* Sincronização automatizada de arquivos alterados para a instância de desenvolvimento AEM.
* Sincronização bidirecional manual de arquivos e pastas.
* Sincronização completa do pacote de conteúdo do projeto.
* Autocompletar de código HTL para expressões e `data-sly-*` instruções em bloco.

Além disso, o Brackets vem com muitos recursos úteis para desenvolvedores de front-end AEM:

* Suporte a arquivos Photoshop para extrair informações de um arquivo PSD, como camadas, medidas, cores, fontes, textos e assim por diante.
* Dicas de código do PSD, para reutilizar facilmente essas informações extraídas no código.
* Suporte ao pré-processador de CSS, como MENOS e SCSS.
* E centenas de extensões adicionais que cobrem necessidades mais específicas.

## Instalação {#installation}

### Colchetes {#brackets}

A extensão AEM Brackets é compatível com a versão 1.0 ou superior do Brackets.

Baixe a versão mais recente do Brackets em [colchetes.io](https://brackets.io/).

### A extensão {#the-extension}

Para instalar a extensão, proceda da seguinte maneira:

1. Colchetes. No menu **Arquivo**, selecione **Extension Manager...**
1. Enter **AEM** na barra de pesquisa e procure **Extensão de Colchetes AEM**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Clique em **Instalar**.
1. Feche a caixa de diálogo e o Extension Manager após a conclusão da instalação.

## Introdução {#getting-started}

### O projeto do pacote de conteúdo {#the-content-package-project}

Depois que a extensão for instalada, você poderá começar a desenvolver componentes do AEM abrindo uma pasta de pacote de conteúdo no seu sistema de arquivos com o Brackets.

O projeto deve conter pelo menos:

1. a `jcr_root` pasta (por exemplo, `myproject/jcr_root`)

1. a `filter.xml` arquivo (por exemplo, `myproject/META-INF/vault/filter.xml`); para obter mais detalhes sobre a estrutura do `filter.xml` arquivo consulte o [Definição de filtro do Workspace](https://jackrabbit.apache.org/filevault/filter.html).

Entre parênteses&#39; **Arquivo** escolha **Abrir pasta...** e escolha a opção `jcr_root` ou a pasta do projeto principal.

>[!NOTE]
>
>Se você não tiver um projeto próprio com um pacote de conteúdo, poderá tentar o [Exemplo de HTL TodoMVC](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). No GitHub, clique em **Fazer download do ZIP**, extraia os arquivos localmente e, conforme instruído acima, abra o `jcr_root` pasta entre colchetes. Siga as etapas abaixo para configurar o **Configurações do projeto** e, por fim, faça o upload de todo o pacote para a sua instância de desenvolvimento do AEM fazendo uma **Exportar pacote de conteúdo** conforme instruído na seção Sincronização completa do pacote de conteúdo.
>
>Após essas etapas, você poderá acessar a variável `/content/todo.html` URL na instância de desenvolvimento do AEM e você pode começar a fazer modificações no código entre parênteses e ver como, após uma atualização no navegador da Web, as alterações foram imediatamente sincronizadas com o servidor AEM.

### Configurações do projeto {#project-settings}

Para sincronizar seu conteúdo de e para uma instância de desenvolvimento AEM, é necessário definir as Configurações do projeto. Isso pode ser feito acessando o **AEM** e escolhendo **Configurações do projeto...**

![chlimage_1-55](assets/chlimage_1-55a.png)

As Configurações do projeto permitem definir o seguinte:

1. O URL do servidor (por exemplo, `http://localhost:4502`)
1. Tolerar servidores que não tenham um certificado HTTPS válido (manter desmarcado, a menos que necessário)
1. O nome de usuário usado para sincronizar conteúdo (por exemplo, `admin`)
1. A senha do usuário (por exemplo, `admin`)

## Sincronização de conteúdo {#synchronizing-content}

A extensão AEM Brackets fornece os seguintes tipos de sincronização de conteúdo para arquivos e pastas permitidos pelas regras de filtragem definidas no `filter.xml`:

### Sincronização Automatizada De Arquivos Alterados {#automated-synchronization-of-changed-files}

Isso só sincronizará as alterações entre Colchetes e a instância AEM, mas nunca o contrário.

### Sincronização Bidirecional Manual {#manual-bidirectional-synchronization}

No Project Explorer, abra o menu contextual clicando com o botão direito do mouse em qualquer arquivo ou pasta e **Exportar para o servidor** ou **Importar do servidor** opções podem ser acessadas.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Se a entrada selecionada estiver fora do `jcr_root` pasta, a variável **Exportar para o servidor** e **Importar do servidor** as entradas de menu contextuais estão desativadas.

### Sincronização completa do pacote de conteúdo {#full-content-package-synchronization}

No **AEM** menu, a caixa **Exportar pacote de conteúdo** ou **Importar pacote de conteúdo** As opções permitem sincronizar todo o projeto com o servidor.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Status da sincronização {#synchronization-status}

A extensão AEM Brackets apresenta um ícone de notificação na barra de ferramentas à direita da janela Brackets, que indica o status da última sincronização:

* verde - todos os arquivos foram sincronizados com êxito
* azul - uma operação de sincronização está em andamento
* amarelo - alguns dos arquivos não foram sincronizados
* vermelho - nenhum dos arquivos foi sincronizado

Clicar no ícone de notificação abre a caixa de diálogo Status da sincronização, que lista todos os status de cada arquivo sincronizado.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Somente conteúdo marcado como incluído pelas regras de filtragem de `filter.xml` serão sincronizados, independentemente do método de sincronização usado.
>
>Além disso, `.vltignore` os arquivos são suportados para excluir conteúdo da sincronização para e do repositório.

## Edição do código HTL {#editing-htl-code}

A extensão Colchetes AEM também apresenta preenchimento automático para facilitar a gravação de atributos e expressões HTL.

### Preenchimento automático do atributo {#attribute-auto-completion}

1. Em um atributo HTML, digite `sly`. O atributo é preenchido automaticamente para `data-sly-`.
1. Selecione o atributo HTL na lista suspensa.

### Preenchimento automático da expressão {#expression-auto-completion}

Em uma expressão `${}`, os nomes de variáveis comuns são preenchidos automaticamente.

## Mais informações {#more-information}

A extensão AEM Brackets é um projeto de código aberto, hospedado no GitHub pela [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) sob a licença Apache, versão 2.0:

* Repositório de código: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licença do Apache, versão 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

O editor de código Brackets também é um projeto de código aberto, hospedado no GitHub pela [Adobe Systems Incorporated](https://github.com/adobe) organização:

* Repositório de código: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

Sinta-se à vontade para contribuir!

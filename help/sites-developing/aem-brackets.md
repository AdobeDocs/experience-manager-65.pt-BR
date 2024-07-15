---
title: Extensão de Colchetes AEM
description: Saiba como usar a extensão Adobe Experience Manager para Colchetes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Extensão de Colchetes AEM{#aem-brackets-extension}

## Visão geral {#overview}

A extensão AEM Brackets fornece um fluxo de trabalho suave para editar componentes AEM e bibliotecas de clientes e usa o poder do editor de código [Brackets](https://brackets.io/), que dá acesso a arquivos e camadas do Photoshop a partir do editor de código. A fácil sincronização fornecida pela extensão (sem a necessidade de Maven ou File Vault) aumenta a eficiência do desenvolvedor e também ajuda desenvolvedores de front-end com conhecimento limitado em AEM a participar de projetos. Esta extensão também fornece algum suporte para a [Linguagem de modelo de HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR), que elimina a complexidade do JSP para tornar o desenvolvimento de componentes mais fácil e seguro.

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

Baixe a versão mais recente do Brackets em [brackets.io](https://brackets.io/).

### A extensão {#the-extension}

Para instalar a extensão, proceda da seguinte maneira:

1. Colchetes. No menu **Arquivo**, selecione **Extension Manager...**
1. Insira **AEM** na barra de pesquisa e procure a **Extensão de Colchetes AEM**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Clique em **Instalar**.
1. Feche a caixa de diálogo e o Extension Manager após a conclusão da instalação.

## Introdução {#getting-started}

### O projeto do pacote de conteúdo {#the-content-package-project}

Depois que a extensão for instalada, você poderá começar a desenvolver componentes do AEM abrindo uma pasta de pacote de conteúdo no seu sistema de arquivos com o Brackets.

O projeto deve conter pelo menos:

1. uma pasta `jcr_root` (por exemplo, `myproject/jcr_root`)

1. um arquivo `filter.xml` (por exemplo, `myproject/META-INF/vault/filter.xml`); para obter mais detalhes sobre a estrutura do arquivo `filter.xml`, consulte a [definição de Filtro do Workspace](https://jackrabbit.apache.org/filevault/filter.html).

No menu **Arquivo** do Brackets, escolha **Abrir Pasta...** e escolha a pasta `jcr_root` ou a pasta do projeto pai.

>[!NOTE]
>
>Se você não tiver um projeto próprio com um pacote de conteúdo, tente o [HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). No GitHub, clique em **Baixar ZIP**, extraia os arquivos localmente e, conforme instruído acima, abra a pasta `jcr_root` entre colchetes. Siga as etapas abaixo para configurar as **Configurações do Projeto** e, por fim, carregue o pacote inteiro para a instância de desenvolvimento do AEM fazendo um **Exportar Pacote de Conteúdo**, conforme instruído na seção Sincronização Completa do Pacote de Conteúdo.
>
>Após essas etapas, você poderá acessar a URL `/content/todo.html` na instância de desenvolvimento do AEM e começar a fazer modificações no código entre colchetes e ver como, após uma atualização no navegador da Web, as alterações foram imediatamente sincronizadas com o servidor AEM.

### Configurações do projeto {#project-settings}

Para sincronizar seu conteúdo de e para uma instância de desenvolvimento AEM, é necessário definir as Configurações do projeto. Isso pode ser feito ao acessar o menu **AEM** e escolher **Configurações do Projeto...**

![chlimage_1-55](assets/chlimage_1-55a.png)

As Configurações do projeto permitem definir o seguinte:

1. A URL do servidor (por exemplo, `http://localhost:4502`)
1. Tolerar servidores que não tenham um certificado HTTPS válido (manter desmarcado, a menos que necessário)
1. O nome de usuário usado para sincronizar conteúdo (por exemplo, `admin`)
1. A senha do usuário (por exemplo, `admin`)

## Sincronização de conteúdo {#synchronizing-content}

A Extensão Colchetes AEM fornece os seguintes tipos de sincronização de conteúdo para arquivos e pastas permitidos pelas regras de filtragem definidas em `filter.xml`:

### Sincronização Automatizada De Arquivos Alterados {#automated-synchronization-of-changed-files}

Isso só sincronizará as alterações entre Colchetes e a instância AEM, mas nunca o contrário.

### Sincronização Bidirecional Manual {#manual-bidirectional-synchronization}

No Project Explorer, abra o menu contextual clicando com o botão direito do mouse em qualquer arquivo ou pasta, e as opções **Exportar para Servidor** ou **Importar do Servidor** podem ser acessadas.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Se a entrada selecionada estiver fora da pasta `jcr_root`, as entradas de menu contextual **Exportar para Servidor** e **Importar do Servidor** serão desabilitadas.

### Sincronização completa do pacote de conteúdo {#full-content-package-synchronization}

No menu **AEM**, as opções **Exportar Pacote de Conteúdo** ou **Importar Pacote de Conteúdo** permitem sincronizar todo o projeto com o servidor.

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
>Somente o conteúdo marcado como incluído pelas regras de filtragem de `filter.xml` será sincronizado, independentemente do método de sincronização usado.
>
>Além disso, há suporte para `.vltignore` arquivos para a exclusão de conteúdo da sincronização para e do repositório.

## Edição do código HTL {#editing-htl-code}

A extensão Colchetes AEM também apresenta preenchimento automático para facilitar a gravação de atributos e expressões HTL.

### Preenchimento automático do atributo {#attribute-auto-completion}

1. Em um atributo HTML, digite `sly`. O atributo foi preenchido automaticamente para `data-sly-`.
1. Selecione o atributo HTL na lista suspensa.

### Preenchimento automático da expressão {#expression-auto-completion}

Em uma expressão `${}`, os nomes de variáveis comuns são preenchidos automaticamente.

## Mais informações {#more-information}

A Extensão AEM Brackets é um projeto de código aberto, hospedado no GitHub pela organização [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud), sob a Licença Apache, versão 2.0:

* Repositório de código: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licença do Apache, versão 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

O editor de código Brackets também é um projeto de código aberto, hospedado no GitHub pela organização [Adobe Systems Incorporated](https://github.com/adobe):

* Repositório de código: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

Sinta-se à vontade para contribuir!

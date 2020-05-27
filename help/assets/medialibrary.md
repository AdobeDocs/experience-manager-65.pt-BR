---
title: Compare os ativos Adobe Experience Manager e a oferta de Biblioteca de mídia.
description: Compare os ativos Experience Manager e as ofertas da Biblioteca de mídia e conheça as diferenças.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 2%

---


# Ativos do Experience Manager versus biblioteca de mídia do Experience Manager {#aem-assets-vs-aem-medialibrary}

Os ativos Adobe Experience Manager são parte integrante da plataforma Experience Manager. Essa integração suave é considerada uma grande vantagem do Experience Manager e garante consistência na gestão de conteúdo e alta produtividade para os autores de conteúdo.

## Perguntas frequentes {#frequently-asked-questions}

### O que é o Assets? {#what-is-aem-assets}

O Assets é um recurso do Experience Manager que permite que os usuários gerenciem seus ativos digitais (imagens, vídeos, documentos e clipes de áudio) em um repositório baseado na Web. Os ativos incluem suporte a metadados, execuções, o localizador e a interface de administração.

### O que é a biblioteca de mídia do Experience Manager? {#what-is-the-aem-media-library}

A biblioteca de mídia do Experience Manager é uma parte designada do repositório de conteúdo WCM do Experience Manager, onde as imagens e outros recursos compartilhados são armazenados. A Biblioteca de mídia fornece recursos básicos de gerenciamento de ativos digitais ao WCM.

### O que obtenho dos Ativos que não fazem parte do WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Os recursos exclusivos que estão disponíveis somente para clientes do Assets são:

* a capacidade de extrair e editar metadados diferentes de título, tags e descrição.
* o Administrador de ativos, disponível na tela de boas-vindas.
* todas as etapas do fluxo de trabalho relacionadas ao Gerenciamento de ativos digitais, como ingestão, exclusão de ativos, manipulação de subativos, extração de metadados.
* bibliotecas incluindo `dam` no espaço do pacote.

O uso desses recursos requer uma licença válida do Assets.

### Os ativos estão disponíveis como um pacote separado? {#is-aem-assets-available-as-a-separate-package}

Não. Para facilitar a instalação e a implantação, todos os aplicativos e complementos do Experience Manager são fornecidos em um único pacote com todas as funcionalidades incluídas. Isso não implica que você tenha permissão para usar todos os recursos do pacote.

### Quero editar metadados de ativos digitais. Preciso de ativos? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Se você estiver planejando editar metadados diferentes de título, descrição e tags, é necessário licenciar Ativos.

### Quero usar o predicado de categoria no meu site. Preciso de ativos? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Sim, o predicado de categoria é parte do Assets e requer uma licença do Assets.

### Desejo redimensionar automaticamente as imagens após a importação. Preciso de ativos? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Não. A redimensionamento e a transformação automática, orientada por fluxo de trabalho, de imagens estáticas, bem como a capacidade de gerenciar execuções fazem parte da Biblioteca de mídia do Experience Manager. Esses recursos não exigem uma licença do Assets.

### Desejo redimensionar imagens usando um componente de imagem personalizado. Preciso de ativos? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

O componente de imagem faz parte do WCM. A biblioteca de gráficos que está sendo usada pelo componente de imagem (mas também pelos Ativos) faz parte da plataforma Experience Manager e não exige uma licença dos Ativos.

### Como posso impedir que meus usuários usem os Ativos se eu não tiver licenciado os Ativos? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Você pode remover todos os workflows, componentes, taxonomias, opções e o administrador de Ativos específicos do Experience Manager. Isso evita que os usuários usem acidentalmente os recursos do Assets que você não licenciou.

### Quero adicionar imagens a uma página e cortar e redimensionar essas imagens. Preciso de ativos? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

Nesse caso de uso, não é necessário comprar Ativos, nem mesmo o uso da Biblioteca de mídia é necessário para usar imagens em um site, já que o componente de imagem inteligente permite o upload de imagens diretamente na página.

### Uma lista detalhada dos recursos disponíveis em Ativos vs Biblioteca de mídia {#listoffeatures}

**Experience Manager Assets**

* Coleções e lightbox
* Propriedades e gerenciamento de metadados avançados
* Adobe Asset Link (conectar-se à Creative Cloud para empresas)
* Aplicativo de desktop do Experience Manager
* Processamento de perfis
* [!DNL Adobe InDesign Server] integração
* Modelos de ativos e estrutura de produtores de catálogos
* [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] integração
* Gerenciamento de ativos multilíngues
* Integração de PIM
* Gerenciamento de direitos
* Suporte a Camera RAW
* Gerenciamento e configuração de aspectos de pesquisa
* workflows DAM pré-criados (por exemplo, fotografar)
* relatórios e análise de ativos chamados Insights
* Gerenciamento de ativos 3D
* Connected Assets
* Brand Portal
* Acesso a autoatendimento
* Procurar, pesquisar e baixar
* Coleções e compartilhamento de pastas
* Ferramentas administrativas e interface
* Marcação inteligente
* Pesquisa visual

**Biblioteca de mídia**

* Propriedades básicas de metadados
* Gerenciamento de tags
* Controle de versão
* Representações estáticas
* Projetos, tarefas, criação de fluxo de trabalho
* Atividade (linha do tempo)
* Construtor de Query (API)
* Integração da Marketing Cloud
* Personalização e extensão da interface do usuário
* Comentários e anotações

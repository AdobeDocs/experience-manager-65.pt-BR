---
title: Arquitetura de software
seo-title: Software Architecture
description: Práticas recomendadas para a arquitetura do seu software
seo-description: Best practices for architecting your software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Arquitetura de software{#software-architecture}

## Design para atualizações {#design-for-upgrades}

Ao estender os comportamentos do OOTB, é importante ter em mente as atualizações. Sempre aplique personalizações no diretório /apps e sobreponha os nós correspondentes no diretório /libs ou use sling:resourceSuperType para estender o comportamento pronto para uso. Embora algumas modificações possam ser necessárias para oferecer suporte a uma nova versão de AEM, a nova versão não deve substituir as personalizações caso essa prática seja seguida.

### Reutilizar modelos e componentes sempre que possível {#reuse-template-and-components-when-possible}

Isso permitirá que o site mantenha uma aparência mais consistente e simplifique a manutenção do código. Quando um novo modelo for necessário, certifique-se de estender de um modelo base compartilhado para que os requisitos globais, como a inclusão clientlib, possam ser codificados em um local. Quando um novo componente for necessário, procure oportunidades para se estender a partir de um componente existente.

### Designs de modelo de design {#design-template-designs}

Ao definir quais componentes podem ser incluídos em cada parsys na página, a consistência da aparência do site pode ser controlada. Ao restringir o acesso ao design nas páginas, os &quot;superautores&quot; podem ter permissão para modificar os componentes permitidos por página sem a intervenção do desenvolvedor, garantindo ao mesmo tempo que os outros autores sigam os padrões corporativos.

### Desenvolver uma arquitetura SOLID {#develop-a-solid-architecture}

O SOLID é um acrônimo que descreve cinco princípios arquitetônicos que devem ser respeitados:

* **S** Princípio de responsabilidade única - cada módulo, classe, método, etc. deve ter apenas uma responsabilidade.
* **O** Princípio aberto/fechado - os módulos devem ser abertos para extensão e fechados para modificação.
* **L** Princípio da substituição iskov - os tipos devem ser substituíveis pelos seus subtipos.
* **I** Princípio de segmentação da interface - nenhum cliente deve ser forçado a depender de métodos que não usa.
* **D** Princípio de inversão de dependência - Os módulos de alto nível não devem depender dos módulos de baixo nível. Ambos devem depender de abstrações. As abstrações não devem depender de detalhes. Os detalhes devem depender de abstrações.

O cumprimento destes cinco princípios deve conduzir a um sistema que tenha uma separação rigorosa das preocupações.

>[!TIP]
>
>O SOLID é um conceito comumente utilizado na programação orientada a objetos e cada elemento é amplamente discutido na literatura do setor.
>
>Este é apenas um breve resumo apresentado para conscientização e você é encorajado a se familiarizar com esses conceitos mais a fundo.

### Siga o princípio da robustez {#follow-the-robustness-principle}

O Princípio da Robustez afirma que devemos ser conservadores no que enviamos, mas ser liberais no que aceitamos. Em outras palavras, ao enviar mensagens para terceiros, devemos estar em conformidade total com as especificações, mas ao receber mensagens de terceiros, devemos aceitar mensagens não conformes, desde que o significado da mensagem seja claro.

### Implementar picos em seus próprios módulos {#implement-spikes-in-their-own-modules}

Picos e código de teste são parte integrante de qualquer implementação de software do Agile, mas queremos garantir que eles não entrem em nossa base de código de produção sem o nível apropriado de supervisão. Como resultado, é recomendável criar picos em seu próprio módulo.

### Implementar scripts de migração de dados em seu próprio módulo {#implement-data-migration-scripts-in-their-own-module}

Os scripts de migração de dados, enquanto o código de produção, geralmente são executados apenas uma vez na primeira inicialização de um site. Portanto, assim que o site estiver ativo, isso se torna código inativo. Para garantir que não criemos um código de implementação que dependa dos scripts de migração, eles devem ser implementados em seu próprio módulo. Isso também permite remover e desativar esse código imediatamente após o lançamento, eliminando o código inativo do sistema.

### Siga as convenções Maven publicadas em arquivos POM {#follow-published-maven-conventions-in-pom-files}

O Apache publicou convenções de estilo em [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). É preferível seguir estas convenções, uma vez que facilitará a rápida mobilização de novos recursos.

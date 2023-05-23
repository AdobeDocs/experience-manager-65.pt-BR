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

## Projeto para atualizações {#design-for-upgrades}

Ao estender comportamentos OOTB, é importante ter as atualizações em mente. Sempre aplique personalizações no diretório /apps e sobreponha a parte superior dos nós correspondentes no diretório /libs ou use sling:resourceSuperType para estender o comportamento pronto para uso. Embora algumas modificações possam ser necessárias para suportar uma nova versão do AEM, a nova versão não deve substituir suas personalizações se essa prática for seguida.

### Reutilizar modelo e componentes quando possível {#reuse-template-and-components-when-possible}

Isso permitirá que o site mantenha uma aparência mais consistente e simplifique a manutenção do código. Quando um novo modelo for necessário, estenda de um modelo base compartilhado para que os requisitos globais, como a inclusão da clientlib, possam ser codificados em um local. Quando um novo componente for necessário, procure oportunidades para estender de um componente existente.

### Designs de modelo de design {#design-template-designs}

Ao definir quais componentes podem ser incluídos em cada parsys na página, a consistência da aparência do site pode ser controlada. Restringindo o acesso ao design nas páginas, os &quot;superautores&quot; podem modificar os componentes permitidos por página sem a intervenção do desenvolvedor e, ao mesmo tempo, garantindo que os outros autores sigam os padrões corporativos.

### Desenvolver uma arquitetura SÓLIDA {#develop-a-solid-architecture}

SOLID é um acrônimo que descreve cinco princípios arquitetônicos que devem ser seguidos:

* **S** Princípio de responsabilidade única - cada módulo, classe, método, etc. deve ter apenas uma responsabilidade.
* **O** Princípio de Abertura/Fechamento - os módulos devem ser abertos para extensão e fechados para modificação.
* **L** Princípio de substituição iskov - os tipos devem ser substituíveis por seus subtipos.
* **I** Princípio de segmentação de interface - nenhum cliente deve ser forçado a depender de métodos que não usa.
* **D** Princípio da inversão de dependência - os módulos de alto nível não devem depender dos módulos de baixo nível. Ambos devem depender de abstrações. As abstrações não devem depender de detalhes. Os detalhes devem depender de abstrações.

O esforço para cumprir esses cinco princípios deve resultar em um sistema que tenha uma separação estrita de preocupações.

>[!TIP]
>
>SOLID é um conceito comumente usado em programação orientada a objetos e cada elemento é amplamente discutido na literatura da indústria.
>
>Este é apenas um breve resumo apresentado para conscientização e você é incentivado a familiarizar-se com esses conceitos em mais profundidade.

### Siga o princípio de robustez {#follow-the-robustness-principle}

O Princípio da Robustez afirma que devemos ser conservadores no que enviamos, mas ser liberais no que aceitamos. Em outras palavras, ao enviar mensagens para terceiros, devemos estar em total conformidade com as especificações, mas ao receber mensagens de terceiros, devemos aceitar mensagens não conformes, desde que o significado da mensagem seja claro.

### Implementar picos em seus próprios módulos {#implement-spikes-in-their-own-modules}

Os picos e o código de teste são parte integrante de qualquer implementação de software Agile, mas queremos garantir que eles não cheguem à nossa base de código de produção sem o nível apropriado de supervisão. Como resultado, é recomendável criar picos em seu próprio módulo.

### Implementar scripts de migração de dados em seu próprio módulo {#implement-data-migration-scripts-in-their-own-module}

Os scripts de migração de dados, enquanto o código de produção, geralmente são executados apenas uma vez na primeira inicialização de um site. Portanto, assim que o site estiver ativo, isso se tornará um código inativo. Para garantir que não criemos um código de implementação que dependa dos scripts de migração, eles devem ser implementados em seu próprio módulo. Isso também nos permite remover e desativar esse código imediatamente após o lançamento, eliminando o código inativo do sistema.

### Siga as convenções do Maven publicadas em arquivos POM {#follow-published-maven-conventions-in-pom-files}

O Apache publicou convenções de estilo em [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). É melhor seguir essas convenções, pois facilitará a rápida disponibilização de novos recursos.

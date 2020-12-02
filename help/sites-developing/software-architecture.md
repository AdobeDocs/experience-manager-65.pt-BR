---
title: Arquitetura de software
seo-title: Arquitetura de software
description: Práticas recomendadas para a arquitetura do seu software
seo-description: Práticas recomendadas para a arquitetura do seu software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Arquitetura de software{#software-architecture}

## Design para atualizações {#design-for-upgrades}

Ao estender os comportamentos de OOTB, é importante ter em mente as atualizações. Sempre aplique personalizações no diretório /apps e sobreponha na parte superior dos nós correspondentes no diretório /libs ou use sling:resourceSuperType para estender o comportamento fora da caixa. Embora algumas modificações possam ser necessárias para suportar uma nova versão AEM, a nova versão não deve substituir suas personalizações se esta prática for seguida.

### Reutilizar modelos e componentes quando possível {#reuse-template-and-components-when-possible}

Isso permitirá que o site mantenha uma aparência mais consistente e simplifique a manutenção do código. Quando um novo modelo for necessário, certifique-se de estender de um modelo base compartilhado para que os requisitos globais, como a inclusão clientlib, possam ser codificados em um local. Quando um novo componente for necessário, procure oportunidades para se estender de um componente existente.

### Design de modelos {#design-template-designs}

Ao definir quais componentes podem ser incluídos em cada parsys na página, a consistência da aparência do site pode ser controlada. Ao restringir o acesso ao design nas páginas, os &quot;superautores&quot; podem ser autorizados a modificar os componentes permitidos por página sem a intervenção do desenvolvedor, garantindo ao mesmo tempo que os outros autores sigam os padrões corporativos.

### Desenvolver uma arquitetura SÓLIDA {#develop-a-solid-architecture}

SÓLIDO é um acrônimo que descreve cinco princípios arquitetônicos que devem ser respeitados:

* **Princípio de responsabilidade**&#x200B;única - cada módulo, classe, método, etc., deve fazer apenas uma coisa.
* **Princípio** aberto/fechado - os módulos devem estar abertos para extensão e fechados para modificação.
* **Princípio de substituição de** Liskov Os tipos de substituição devem ser substituíveis pelos seus subtipos.
* **Princípio de segmentação da** interface - nenhum cliente deve ser forçado a depender dos métodos que não usa.
* **Princípio da Inversão de** Dependência - Os módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações. As abstrações não devem depender de detalhes. Os detalhes devem depender de abstrações.

A procura do cumprimento destes cinco princípios deverá resultar num sistema que tenha uma separação rigorosa das preocupações.

### Siga o Princípio da Robustez {#follow-the-robustness-principle}

O Princípio da Robusteza diz que devemos ser conservadores no que enviamos, mas ser liberais no que aceitamos. Por outras palavras, ao enviar mensagens a terceiros, devemos estar completamente em conformidade com as especificações, mas ao receber mensagens de terceiros, devemos aceitar mensagens não conformes, desde que o significado da mensagem seja claro.

### Implementar picos em seus próprios módulos {#implement-spikes-in-their-own-modules}

Os picos e o código de teste são parte integrante de qualquer implementação de software Ágil, mas queremos garantir que eles não entrem em nossa base de código de produção sem o nível adequado de supervisão. Como resultado, é recomendável criar picos em seu próprio módulo.

### Implementar scripts de migração de dados em seu próprio módulo {#implement-data-migration-scripts-in-their-own-module}

Os scripts de migração de dados, enquanto o código de produção, geralmente são executados apenas uma vez na primeira inicialização de um site. Portanto, assim que o site estiver ao vivo, isso se torna código morto. Para garantir que não criemos um código de implementação que dependa dos scripts de migração, eles devem ser implementados em seu próprio módulo. Isso também permite remover e desativar esse código imediatamente após a inicialização, eliminando o código morto do sistema.

### Siga as convenções Maven publicadas em arquivos POM {#follow-published-maven-conventions-in-pom-files}

O Apache publicou convenções de estilo em [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). É preferível seguir estas convenções, uma vez que facilitará a rápida mobilização de novos recursos.

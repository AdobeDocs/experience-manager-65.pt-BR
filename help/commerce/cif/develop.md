---
title: Desenvolver AEM Commerce
description: Saiba como gerar um projeto de AEM habilitado para comércio usando o arquétipo de projeto AEM. Saiba como criar e implantar o projeto em um ambiente de desenvolvimento local.
topics: Commerce, Development
feature: Estrutura de integração de comércio
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 32%

---


# Desenvolvimento do AEM Commerce {#develop}

O desenvolvimento de projetos AEM Commerce com base na Commerce Integration Framework (CIF) para AEM segue as mesmas regras e práticas recomendadas de outros projetos AEM. Leia primeiro estes itens:

- [Guia do usuário para desenvolvimento no AEM 6.5](/help/sites-developing/home.md)
- [AEM Conceitos principais](/help/sites-developing/the-basics.md)
- [Desenvolvimento de AEM - Diretrizes e práticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Desenvolvimento local para comércio AEM {#local}

Um ambiente de desenvolvimento local é recomendado para trabalhar com projetos da CIF.

>[!NOTE]
>
>As instruções a seguir ajudam a configurar um ambiente de desenvolvimento de AEM local para AEM Commerce (usando a CIF com foco para AEM 6.5). Se estiver usando AEM como Cloud Service, consulte a documentação [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/home.html).

O complemento AEM Commerce para AEM 6.5 também conhecido. O complemento CIF também está disponível para desenvolvimento local e é fornecido como um pacote AEM. Ele pode ser baixado do [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) como um pacote de recursos.

### Software necessário

Devem ser instalados:

- AEM local 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 ou posterior
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 ou mais recente)
- [Nó LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acesso ao complemento CIF

O complemento CIF pode ser baixado no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html), pesquise por ‘complemento AEM Commerce’.

>[!TIP]
>
>Use sempre a versão mais recente do complemento CIF.

### Configuração local

Para desenvolvimento de projeto da CIF local, siga as etapas abaixo e siga o complemento CIF:

1. Obtenha a versão AEM 6.5 e instale o AEM 6.5 Service Pack. O AEM 6.5 Service Pack 7 é necessário, no entanto, recomendamos instalar o último service pack disponível.

1. Descompacte o AEM .jar para criar a pasta `crx-quickstart` e execute:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crie uma pasta `crx-quickstart/install`

1. Copie o complemento CIF de todos os pacotes, baixado do Portal de distribuição de software, na pasta `crx-quickstart/install`.

>[!TIP]
>
>Como alternativa, o pacote complementar da CIF também pode ser instalado por meio do Gerenciador de pacotes.

1. Inicie o início rápido do AEM

Verifique a configuração por meio do console OSGI: `http://localhost:4502/system/console/osgi-installer`. A lista deve incluir os pacotes relacionados ao complemento CIF, o pacote de conteúdo e as configurações OSGI. Certifique-se de que todos os pacotes sejam iniciados.

## Configuração do projeto {#project}

Há duas maneiras de iniciar seu projeto do AEM Commerce usando a CIF.

### Usar o Arquétipo de projeto do AEM

O [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) é a principal ferramenta para inicializar um projeto pré-configurado e começar a usar a CIF. Os Componentes principais da CIF e todas as configurações necessárias podem ser incluídos em um projeto gerado com uma opção extra.

>[!TIP]
>
>Use o [Arquétipo de projeto do AEM 25 ou posterior](https://github.com/adobe/aem-project-archetype/releases) para gerar o projeto.

Consulte as [instruções de uso](https://github.com/adobe/aem-project-archetype#usage) do Arquétipo de projeto do AEM sobre como gerar um projeto do AEM. Para incluir a CIF no projeto, use a opção `includeCommerce`.

Por exemplo:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

Os Componentes principais da CIF podem ser usados em qualquer projeto, incluindo o pacote `all` fornecido ou o indivíduo, usando o pacote de conteúdo da CIF e os pacotes OSGI relacionados. Para adicionar os Componentes principais da CIF manualmente a um projeto, use as seguintes dependências:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Usar a loja de referência AEM Venia

Uma segunda opção para iniciar um projeto da CIF é clonar e usar a [loja de referência AEM Venia](https://github.com/adobe/aem-cif-guides-venia). A loja de referência AEM Venia é um exemplo de aplicativo de vitrine de referência que demonstra o uso dos Componentes principais da CIF para o AEM. Ela serve como um conjunto de exemplos de práticas recomendadas e um ponto de partida potencial para desenvolver sua própria funcionalidade.

Para começar a usar a loja de referência Venia, basta clonar o [repositório Git](https://github.com/adobe/aem-cif-guides-venia) e começar a personalizar o projeto de acordo com suas necessidades.

>[!NOTE]
>
>O projeto da loja de referência Venia contém dois perfis de construção para o AEM as a Cloud Service e o AEM 6.5. Verifique o arquivo [readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) do projeto para ver como eles são usados. Para AEM 6.5, use o perfil `classic` .

### Conectar AEM ao sistema de comércio

Para conectar seu projeto ao sistema de comércio, AEM deve ser configurado com o ponto de extremidade GraphQL do sistema de comércio.

Ambos, um projeto gerado pelo [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) ou pelo [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia), já inclui uma [configuração padrão](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.grafql.client.impl.GraphqlClientImpl~default.cfg.json) que deve ser ajustada.

Substitua o valor de `url` em `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` pelo ponto de extremidade GraphQL do sistema de comércio usado pelo projeto.

O complemento AEM Commerce e os Componentes principais da CIF se conectam ao ponto de extremidade GraphQL de comércio por meio do servidor AEM e diretamente pelo navegador. Por padrão, os Componentes principais da CIF do lado do cliente e as ferramentas de criação do complemento CIF se conectam ao `/api/graphql`. Se necessário, isso pode ser ajustado através da configuração do Cloud Service da CIF (veja abaixo).

O complemento CIF fornece um servlet proxy GraphQL em `/api/graphql`. Se você não planeja usar um Dispatcher de AEM local, é recomendável configurar também o servlet proxy GraphQL.

Navegue até http://localhost:4502/system/console/configMgr e crie uma configuração OSGI para o serviço `Adobe CIF GraphQL Proxy Configuration`. Use o mesmo ponto de extremidade GraphQL do sistema de comércio usado para o cliente GraphQL acima.

## Recursos adicionais

- [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
- [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)

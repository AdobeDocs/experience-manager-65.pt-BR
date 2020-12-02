---
title: Criando Filtros de Grupos de Dispositivos
seo-title: Criando Filtros de Grupos de Dispositivos
description: Criar um filtro de grupo de dispositivos para definir um conjunto de requisitos de capacidade do dispositivo
seo-description: Criar um filtro de grupo de dispositivos para definir um conjunto de requisitos de capacidade do dispositivo
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---


# Criando Filtros de Grupo de Dispositivos{#creating-device-group-filters}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Crie um filtro de grupo de dispositivos para definir um conjunto de requisitos de capacidade do dispositivo. Crie quantos filtros forem necessários para público alvo dos grupos necessários de recursos do dispositivo.

Projete seus filtros para que você possa usar combinações deles para definir os grupos de recursos. Normalmente, há sobreposição dos recursos de diferentes grupos de dispositivos. Portanto, você pode usar alguns filtros com várias definições de grupos de dispositivos.

Depois de criar um filtro, você pode usá-lo na configuração de [grupo.](/help/sites-developing/mobile.md#creating-a-device-group)

## A Classe Java de Filtro {#the-filter-java-class}

Um filtro de grupo de dispositivos é um componente OSGi que implementa a interface [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html). Quando implantada, a classe de implementação fornece um serviço de filtro que está disponível para configurações de grupos de dispositivos.

A solução descrita neste artigo usa o plug-in Apache Felix Maven SCR para facilitar o desenvolvimento do componente e do serviço. Portanto, a classe Java de exemplo usa as anotações `@Component`e `@Service`. A classe tem a seguinte estrutura:

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
public class myDeviceGroupFilter implements DeviceGroupFilter {

       public String getDescription() {
  return null;
 }

 public String getTitle() {
  return null;
 }

 public boolean matches(DeviceGroup arg0, String arg1, Map arg2) {
  return false;
 }

}
```

É necessário fornecer código para os seguintes métodos:

* `getDescription`: Retorna a descrição do filtro. A descrição é exibida na caixa de diálogo de configuração do Grupo de dispositivos.
* `getTitle`: Retorna o nome do filtro. O nome é exibido ao selecionar filtros para o grupo de dispositivos.
* `matches`: Determina se o dispositivo tem os recursos necessários.

### Fornecer o nome e a descrição do filtro {#providing-the-filter-name-and-description}

Os métodos `getTitle` e `getDescription` retornam o nome e a descrição do filtro, respectivamente. O código a seguir ilustra a implementação mais simples:

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

A codificação do texto do nome e da descrição é suficiente para ambientes de criação unidilingues. Considere a externalização das strings para uso multilíngue ou para permitir a alteração de strings sem recompilar o código fonte.

### Avaliando com base nos critérios de filtragem {#evaluating-against-filter-criteria}

A função `matches` retornará `true` se os recursos do dispositivo atenderem a todos os critérios de filtragem. Avalie as informações fornecidas nos argumentos do método para determinar se o dispositivo pertence ao grupo. Os valores a seguir são fornecidos como argumentos:

* Um objeto DeviceGroup
* O nome do agente do usuário
* Um objeto Map que contém os recursos do dispositivo. As chaves do mapa são os nomes dos recursos WURFL™ e os valores são os valores correspondentes do banco de dados WURFL™.

A interface [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) contém um subconjunto dos nomes dos recursos WURFL™ em campos estáticos. Use essas constantes de campo como chaves ao recuperar valores do Mapa de recursos do dispositivo.

Por exemplo, o exemplo de código a seguir determina se o dispositivo suporta CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

O pacote `org.apache.commons.lang.math` fornece a classe `NumberUtils`.

>[!NOTE]
>
>Verifique se o banco de dados WURFL™ implantado no AEM inclui os recursos que você usa como critérios de filtragem. (Consulte [Detecção de Dispositivo](/help/sites-developing/mobile.md#server-side-device-detection).)

### Exemplo de filtro para tamanho de tela {#example-filter-for-screen-size}

O exemplo de implementação DeviceGroupFilter a seguir determina se o tamanho físico do dispositivo atende aos requisitos mínimos. Esse filtro destina-se a adicionar granularidade ao grupo de dispositivos de toque. O tamanho dos botões na interface do usuário do aplicativo deve ser o mesmo, independentemente do tamanho físico da tela. O tamanho de outros itens, como texto, pode variar. O filtro permite a seleção dinâmica de um CSS específico que controla o tamanho dos elementos da interface.

Esse filtro aplica critérios de tamanho aos nomes das propriedades `physical_screen_height` e `physical_screen_width` WURFL™.

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.commons.lang.math.NumberUtils;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
@SuppressWarnings("unused")
public class ScreenSizeLarge implements DeviceGroupFilter {
    private int len=400;
    private int wid=200;
    public String getDescription() {

        return "Requires the physical size of the screen to have minimum dimensions " + len + "x" + wid+".";
    }

    public String getTitle() {
        return "Screen Size Large ("+len + "x" + wid+")";
    }

    public boolean matches(DeviceGroup deviceGroup, String userAgent,
            Map<String, String> deviceCapabilities) {

        boolean longEnough=true;
        boolean wideEnough=false;
        int dimension1=NumberUtils.toInt(deviceCapabilities.get("physical_screen_height"));
        int dimension2=NumberUtils.toInt(deviceCapabilities.get("physical_screen_width"));
        if(dimension1>dimension2){
            longEnough=dimension1>=len;
            wideEnough=dimension2>=wid;
        }else{
            longEnough=dimension2>=len;
            wideEnough=dimension1>=wid;
        }

        return longEnough && wideEnough;
    }
}
```

O valor String retornado pelo método getTitle aparece na lista suspensa das propriedades do grupo de dispositivos.

![filteraddtogroup](assets/filteraddtogroup.png)

Os valores String que os métodos getTitle e getDescription retornam são incluídos na parte inferior da página de resumo do grupo de dispositivos.

![filterdescription](assets/filterdescription.png)

### O arquivo Maven POM {#the-maven-pom-file}

O seguinte código POM é útil se você usar o Maven para criar seus aplicativos. O POM faz referência a vários plug-ins e dependências necessários.

**Plug-ins:**

* Plug-in Apache Maven Compiler: Compila classes Java do código-fonte.
* Plug-in Apache Felix Maven Bundle: Cria o pacote e o manifesto
* Plug-in Apache Felix Maven SCR: Cria o arquivo descritor do componente e configura o cabeçalho do manifesto service-component.

**Dependências:**

* `cq-wcm-mobile-api-5.5.2.jar`: Fornece as interfaces DeviceGroup e DeviceGroupFilter.

* `org.apache.felix.scr.annotations.jar`: Fornece as anotações Componente e Serviço.

As interfaces DeviceGroup e DeviceGroupFilter estão incluídas no pacote de API do Day Communique 5 WCM Mobile. As anotações do Felix estão incluídas no pacote Apache Felix Declarative Services. Você pode obter esse arquivo JAR do repositório Adobe público.

No momento da criação, 5.5.2 é a versão do pacote de API do WCM Mobile que está na versão mais recente do AEM. Use o Console Web do Adobe ([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)) para garantir que esta seja a versão do pacote implantada no seu ambiente.

**POM:** (seu POM usará uma groupId e uma versão diferentes.)

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.adobe.example.myapp</groupId>
      <artifactId>devicefilter</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>my app device filter</name>
      <url>https://dev.day.com/docs/en/cq/current.html</url>
  <packaging>bundle</packaging>
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-scr-plugin</artifactId>
            <executions>
                  <execution>
                    <id>generate-scr-scrdescriptor</id>
                    <goals>
                          <goal>scr</goal>
                    </goals>
                  </execution>
            </executions>
          </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
    </plugins>
</build>
<dependencies>
     <dependency>
         <groupId>com.day.cq.wcm</groupId>
         <artifactId>cq-wcm-mobile-api</artifactId>
         <version>5.5.2</version>
         <scope>provided</scope>
     </dependency>
     <dependency>
        <groupId>org.apache.felix</groupId>
        <artifactId>org.apache.felix.scr.annotations</artifactId>
        <version>1.6.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
</project>
```

Adicione o perfil que a seção [Obtenção do Plug-in Content Package Maven](/help/sites-developing/vlt-mavenplugin.md) fornece ao seu arquivo de configurações maven para usar o repositório Adobe público.

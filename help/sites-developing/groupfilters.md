---
title: Criando Filtros de Grupo de Dispositivos
seo-title: Creating Device Group Filters
description: Crie um filtro de grupo de dispositivos para definir um conjunto de requisitos de capacidade do dispositivo
seo-description: Create a device group filter to define a set of device capability requirements
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
exl-id: 419d2e19-1198-4ab5-9aa0-02ad18fe171d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Criando Filtros de Grupo de Dispositivos{#creating-device-group-filters}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Crie um filtro de grupo de dispositivos para definir um conjunto de requisitos de capacidade do dispositivo. Crie quantos filtros forem necessários para direcionar os grupos necessários de recursos do dispositivo.

Crie seus filtros para que você possa usar combinações deles para definir os grupos de recursos. Normalmente, há uma sobreposição dos recursos de diferentes grupos de dispositivos. Portanto, você pode usar alguns filtros com várias definições de grupo de dispositivos.

Depois de criar um filtro, você pode usá-lo no [configuração de grupo.](/help/sites-developing/mobile.md#creating-a-device-group)

## A Classe Java do Filtro {#the-filter-java-class}

Um filtro de grupo de dispositivos é um componente OSGi que implementa o [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) interface. Quando implantada, a classe de implementação fornece um serviço de filtro que está disponível para configurações de grupos de dispositivos.

A solução descrita neste artigo usa o plug-in SCR do Apache Felix Maven para facilitar o desenvolvimento do componente e do serviço. Portanto, a classe Java de exemplo usa a variável `@Component`e `@Service` anotações. A classe tem a seguinte estrutura:

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

Você precisa fornecer um código para os seguintes métodos:

* `getDescription`: Retorna a descrição do filtro. A descrição é exibida na caixa de diálogo Configuração do grupo de dispositivos .
* `getTitle`: Retorna o nome do filtro. O nome aparece ao selecionar filtros para o grupo de dispositivos.
* `matches`: Determina se o dispositivo tem os recursos necessários.

### Fornecer o nome e a descrição do filtro {#providing-the-filter-name-and-description}

O `getTitle` e `getDescription` métodos retornam o nome e a descrição do filtro, respectivamente. O código a seguir ilustra a implementação mais simples:

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

A codificação rígida do texto de nome e descrição é suficiente para ambientes de criação unidilingues. Considere a externalização das cadeias de caracteres para uso em várias línguas ou a ativação da alteração de cadeias de caracteres sem recompilar o código-fonte.

### Avaliação Em Relação Aos Critérios De Filtro {#evaluating-against-filter-criteria}

O `matches` retornos da função `true` se os recursos do dispositivo atenderem a todos os critérios de filtro. Avalie as informações fornecidas nos argumentos do método para determinar se o dispositivo pertence ao grupo. Os seguintes valores são fornecidos como argumentos:

* Um objeto DeviceGroup
* O nome do agente do usuário
* Um objeto de mapa que contém os recursos do dispositivo. As chaves Map são os nomes de recursos WURFL™ e os valores são os valores correspondentes do banco de dados WURFL™.

O [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) A interface contém um subconjunto dos nomes de recursos WURFL™ em campos estáticos. Use essas constantes de campo como chaves ao recuperar valores do Mapa de recursos do dispositivo.

Por exemplo, o exemplo de código a seguir determina se o dispositivo suporta CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

O `org.apache.commons.lang.math` O pacote fornece `NumberUtils` classe .

>[!NOTE]
>
>Verifique se o banco de dados WURFL™ implantado no AEM inclui os recursos que você usa como critério de filtro. (Consulte [Detecção de dispositivo](/help/sites-developing/mobile.md#server-side-device-detection).)

### Exemplo De Filtro Para Tamanho De Tela {#example-filter-for-screen-size}

O exemplo de implementação de DeviceGroupFilter a seguir determina se o tamanho físico do dispositivo atende aos requisitos mínimos. Este filtro destina-se a adicionar granularidade ao grupo de dispositivos de toque. O tamanho dos botões na interface do usuário do aplicativo deve ser o mesmo, independentemente do tamanho físico da tela. O tamanho de outros itens, como texto, pode variar. O filtro permite a seleção dinâmica de um CSS específico que controla o tamanho dos elementos da interface do usuário.

Esse filtro aplica critérios de tamanho à variável `physical_screen_height` e `physical_screen_width` Nomes de propriedades WURFL™.

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

Os valores de String retornados pelos métodos getTitle e getDescription estão incluídos na parte inferior da página de resumo do grupo de dispositivos.

![filterdescription](assets/filterdescription.png)

### O arquivo POM Maven {#the-maven-pom-file}

O seguinte código POM é útil se você usar o Maven para criar seus aplicativos. O POM faz referência a vários plug-ins e dependências necessários.

**Plug-ins:**

* Plug-in do Apache Maven Compiler: Compila classes Java do código-fonte.
* Plug-in do pacote Apache Felix Maven: Cria o pacote e o manifesto
* Plug-in SCR do Apache Felix Maven: Cria o arquivo de descritor de componente e configura o cabeçalho de manifesto service-component.

**Dependências:**

* `cq-wcm-mobile-api-5.5.2.jar`: Fornece as interfaces DeviceGroup e DeviceGroupFilter .

* `org.apache.felix.scr.annotations.jar`: Fornece as anotações Componente e Serviço .

As interfaces DeviceGroup e DeviceGroupFilter estão incluídas no pacote de API móvel do Day Communique 5 WCM. As anotações Felix estão incluídas no pacote Apache Felix Declarative Services. Você pode obter esse arquivo JAR do repositório do Adobe público.

No momento da criação, 5.5.2 é a versão do pacote de API do WCM Mobile que está na versão mais recente do AEM. Use o Console da Web do Adobe ([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)) para garantir que essa seja a versão do pacote implantada em seu ambiente.

**POM:** (O POM usará uma groupId e uma versão diferentes.)

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

Adicione o perfil que a função [Obter o plug-in Content Package Maven](/help/sites-developing/vlt-mavenplugin.md) seção fornece ao arquivo de configurações maven para usar o repositório Adobe público.

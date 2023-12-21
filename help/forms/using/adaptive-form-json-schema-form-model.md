---
title: Como criar Forms adaptável usando o esquema JSON?
description: Saiba como criar formulários adaptáveis usando o esquema JSON como modelo de formulário. Você pode usar esquemas JSON existentes para criar formulários adaptáveis. Saiba mais com uma amostra de um esquema JSON, pré-configure campos na definição do esquema JSON, limite valores aceitáveis para um componente de formulário adaptável e aprenda construções não compatíveis.
role: User, Developer
level: Beginner, Intermediate
feature: Adaptive Forms, Foundation Components
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 4%

---

# Criação de formulários adaptáveis usando o esquema JSON {#creating-adaptive-forms-using-json-schema}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) |
| AEM 6.5 | Este artigo |


## Pré-requisitos {#prerequisites}

A criação de um formulário adaptável usando um Esquema JSON como seu modelo de formulário requer compreensão básica do Esquema JSON. É recomendável ler o conteúdo a seguir antes deste artigo.

* [Criação de um formulário adaptável](creating-adaptive-form.md)
* [Esquema JSON](https://json-schema.org/)

## Utilização de um esquema JSON como modelo de formulário  {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] O oferece suporte à criação de um formulário adaptável usando um Esquema JSON existente como o modelo de formulário. Esse esquema JSON representa a estrutura em que os dados são produzidos ou consumidos pelo sistema de back-end em sua organização. O esquema JSON usado deve ser compatível com [Especificações da v4](https://json-schema.org/draft-04/schema).

Os principais recursos do uso de um Esquema JSON são:

* A estrutura do JSON é exibida como uma árvore na guia Localizador de conteúdo no modo de criação de um formulário adaptável. Você pode arrastar e adicionar elemento da hierarquia JSON ao formulário adaptável.
* Você pode preencher previamente o formulário usando o JSON compatível com o esquema associado.
* No envio, os dados inseridos pelo usuário são enviados como JSON, que se alinha ao esquema associado.

Um Esquema JSON consiste em tipos de elementos simples e complexos. Os elementos têm atributos que adicionam regras ao elemento. Quando esses elementos e atributos são arrastados para um formulário adaptável, eles são mapeados automaticamente para o componente de formulário adaptável correspondente.

Esse mapeamento de elementos JSON com componentes de formulário adaptáveis é o seguinte:

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>Elemento JSON, propriedades ou atributos</strong></th>
   <th><strong>Componente de formulário adaptável</strong></th>
  </tr>
  <tr>
   <td><p>Propriedades de string com restrições enum e enumNames.</p> <p>Sintaxe,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Componente suspenso:</p>
    <ul>
     <li>Os valores listados em enumNames são exibidos na caixa suspensa.</li>
     <li>Os valores listados na enumeração são usados para cálculo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Propriedade de cadeia de caracteres com restrição de formato. Por exemplo, email e data.</p> <p>Sintaxe,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>O componente de email é mapeado quando o tipo é string e o formato é email.</li>
     <li>O componente Caixa de texto com validação é mapeado quando o tipo é string e o formato é hostname.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> Campo de texto<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>propriedade number<br /> </td>
   <td>Campo numérico com subtipo definido como flutuante<br /> </td>
  </tr>
  <tr>
   <td>propriedade integer<br /> </td>
   <td>Campo numérico com subtipo definido como número inteiro<br /> </td>
  </tr>
  <tr>
   <td>propriedade booleana<br /> </td>
   <td>Alternar<br /> </td>
  </tr>
  <tr>
   <td>propriedade do objeto<br /> </td>
   <td>Painel<br /> </td>
  </tr>
  <tr>
   <td>propriedade de matriz</td>
   <td>Painel repetível com mín. e máx. iguais a minItems e maxItems, respectivamente. Somente matrizes homogêneas são compatíveis. Portanto, a restrição de itens deve ser um objeto e não uma matriz.<br /> </td>
  </tr>
 </tbody>
</table>

### Propriedades comuns do esquema {#common-schema-properties}

O Formulário adaptável usa as informações disponíveis no Esquema JSON para mapear cada campo gerado. Em especial:

* A variável `title` A propriedade serve como rótulo para os componentes de formulário adaptável.
* A variável `description` é definida como descrição longa para um componente de formulário adaptável.
* A variável `default` A propriedade serve como valor inicial de um campo de formulário adaptável.
* A variável `maxLength` é definida como `maxlength` atributo do componente de campo de texto.
* A variável `minimum`, `maximum`, `exclusiveMinimum`, e `exclusiveMaximum` As propriedades são usadas para o componente Caixa numérica.
* Para oferecer suporte ao intervalo de `DatePicker component` propriedades adicionais do Esquema JSON `minDate` e `maxDate` são fornecidos.
* A variável `minItems` e `maxItems` as propriedades são usadas para restringir o número de itens/campos que podem ser adicionados ou removidos de um componente do painel.
* A variável `readOnly` propriedade define a variável `readonly` atributo de um componente de formulário adaptável.
* A variável `required` marca o campo de formulário adaptável como obrigatório, enquanto no painel (em que o tipo é objeto), os dados JSON enviados finais têm campos com valor vazio que correspondem a esse objeto.
* A variável `pattern` é definida como o padrão de validação (expressão regular) no formulário adaptável.
* A extensão do arquivo de Esquema JSON deve ser mantida em .schema.json. Por exemplo, &lt;filename>.schema.json.

## Exemplo de esquema JSON {#sample-json-schema}

Este é um exemplo de um Esquema JSON.

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### Definições de esquema reutilizáveis {#reusable-schema-definitions}

As chaves de definição são usadas para identificar esquemas reutilizáveis. As definições de esquema reutilizáveis são usadas para criar fragmentos. É semelhante à identificação de tipos complexos em XSD. Um exemplo de Esquema JSON com definições é fornecido abaixo:

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

O exemplo acima define um registro de cliente, em que cada cliente tem um endereço de entrega e de cobrança. A estrutura de ambos os endereços é a mesma — os endereços têm endereço, cidade e estado — portanto, é uma boa ideia não duplicar os endereços. Também facilita a adição e a exclusão de campos para qualquer alteração futura.

## Pré-configuração de campos na definição do esquema JSON {#pre-configuring-fields-in-json-schema-definition}

Você pode usar o **aem:afProperties** propriedade para pré-configurar o campo Esquema JSON para mapear para um componente de formulário adaptável personalizado. Um exemplo está listado abaixo:

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## Configurar scripts ou expressões para objetos de formulário  {#configure-scripts-or-expressions-for-form-objects}

JavaScript é a linguagem de expressão de formulários adaptáveis. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Você pode pré-configurar objetos de formulário para [avaliar uma expressão](adaptive-form-expressions.md) em um evento de formulário.

Use a propriedade aem:afproperties para pré-configurar expressões de formulário adaptáveis ou scripts para componentes de formulário adaptáveis. Por exemplo, quando o evento de inicialização é acionado, o código abaixo define o valor do campo de telefone e imprime um valor no log:

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

Você deve ser um membro do [grupo forms-power-user](forms-groups-privileges-tasks.md) para configurar scripts ou expressões para objeto de formulário. A tabela abaixo lista todos os eventos de script compatíveis com um componente de formulário adaptável.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Componente \ Evento</th>
   <th>inicializar <br /> </th>
   <td>Calcular</td>
   <td>Visibilidade</td>
   <td>Validar</td>
   <td>Habilitado</td>
   <td>Confirmação de valor</td>
   <td>Clique em </td>
   <td>Opções</td>
  </tr>
  <tr>
   <td>Campo de texto</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Campo numérico</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Escalonador numérico</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Botão de opção</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telefone</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Alternar</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Botão</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Caixa de seleção</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Suspenso</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Opção de imagem</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Campo de entrada de data</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Seletor de data</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Email</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Anexo de arquivo</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Imagem</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Painel</td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Ícone de marca de verificação Sim" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Alguns exemplos de uso de eventos em um JSON estão ocultando um campo em inicializar evento e configurando o valor de outro campo em evento de confirmação de valor. Para obter informações detalhadas sobre a criação de expressões para os eventos de script, consulte [Expressões de formulário adaptável](adaptive-form-expressions.md).

Este é o exemplo de código JSON para exemplos mencionados anteriormente.

### Ocultar um campo no evento de inicialização {#hiding-a-field-on-initialize-event}

```json
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configurar o valor de outro campo no evento de confirmação de valor {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## Limitar valores aceitáveis para um componente de formulário adaptável {#limit-acceptable-values-for-an-adaptive-form-component}

Você pode adicionar as seguintes restrições aos elementos do Esquema JSON para limitar os valores aceitáveis para um componente de formulário adaptável:

<table>
 <tbody>
  <tr>
   <td><p><strong> Propriedade do esquema</strong></p> </td>
   <td><p><strong>Tipo de dados</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o limite superior para valores numéricos e datas. Por padrão, o valor máximo é incluído.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador Numérico<br /> </li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o limite inferior para valores numéricos e datas. Por padrão, o valor mínimo é incluído.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, o valor numérico ou a data especificada no componente do formulário deverá ser menor que o valor numérico ou a data especificada para a propriedade máxima.</p> <p>Se false, o valor numérico ou a data especificada no componente do formulário deve ser menor ou igual ao valor numérico ou à data especificada para a propriedade maximum.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, o valor numérico ou a data especificada no componente do formulário deverá ser maior que o valor numérico ou a data especificada para a propriedade minimum.</p> <p>Se false, o valor numérico ou a data especificada no componente do formulário deve ser maior ou igual ao valor numérico ou à data especificada para a propriedade minimum.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o número mínimo de caracteres permitidos em um componente. O comprimento mínimo deve ser igual ou maior que zero.</p> </td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>String</td>
   <td>Especifica o número máximo de caracteres permitidos em um componente. O comprimento máximo deve ser igual ou maior que zero.</td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica a sequência dos caracteres. Um componente aceita os caracteres se eles estiverem em conformidade com o padrão especificado.</p> <p>A propriedade pattern mapeia para o padrão de validação do componente de formulário adaptável correspondente.</p> </td>
   <td>
    <ul>
     <li>Todos os componentes de formulários adaptáveis mapeados para um esquema XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>String</td>
   <td>Especifica o número máximo de itens em uma matriz. O máximo de itens deve ser igual ou maior que zero.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>String</td>
   <td>Especifica o número mínimo de itens em uma matriz. Os itens mínimos devem ser iguais ou maiores que zero.</td>
   <td> </td>
  </tr>
 </tbody>
</table>



## Ativar dados compatíveis com o esquema {#enablig-schema-compliant-data}

Para permitir que todo o Forms adaptável baseado em esquema JSON gere dados compatíveis com o esquema no envio do formulário, siga estas etapas:

1. Acesse o console da Web do Experience Manager em `https://server:host/system/console/configMgr`.
1. Localizar **[!UICONTROL Configuração do canal da Web de comunicação adaptável e interativa]**.
1. Selecione para abrir a configuração no modo de edição.
1. Selecione o **[!UICONTROL Gerar dados compatíveis com o esquema]** caixa de seleção
1. Salve as configurações.

![configuração do canal web de formulário adaptável e comunicação interativa](/help/forms/using/assets/af-ic-web-channel-configuration.png)

## Construções não suportadas  {#non-supported-constructs}

Os formulários adaptáveis não são compatíveis com as seguintes construções de Esquema JSON:

* Tipo nulo
* Tipos de união, como qualquer um, e
* OneOf, AnyOf, AllOf e NOT
* Somente matrizes homogêneas são compatíveis. Portanto, a restrição de itens deve ser um objeto e não uma matriz.

## Perguntas frequentes {#frequently-asked-questions}

**Por que não consigo arrastar elementos individuais de um subformulário (estrutura gerada de qualquer tipo complexo) para subformulários repetíveis (os valores minOccours ou maxOccurs são maiores que 1)?**

Em um subformulário repetível, você deve usar o subformulário completo. Se desejar apenas campos seletivos, use a estrutura inteira e exclua os indesejados.

**Tenho uma estrutura complexa longa no Localizador de conteúdo. Como posso encontrar um elemento específico?**

Você tem duas opções:

* Rolar pela estrutura de árvore
* Use a caixa Pesquisar para localizar um elemento

**Qual deve ser a extensão do arquivo de esquema JSON?**

A extensão do arquivo de esquema JSON deve ser .schema.json. Por exemplo, &lt;filename>.schema.json.

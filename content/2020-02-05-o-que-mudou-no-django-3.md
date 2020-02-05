+++
title = "O que mudou no Django 3.0?"
date = 2020-02-05T01:10:00Z
draft = false
description = """
No Django 3.0 foi iniciado o suporte para tornar o django totalmente async, fornecendo suporte para execução como um aplicativo ASGI, e muito mais.
"""
+++

Segue abaixo a lista do que a de novo do Django 3.0.

### Compatibilidade com Python
O Django 3.0 suporta Python 3.6, 3.7 e 3.8. É altamente recomendável utilizar a versão mais recente de cada série.

No Django 2.2.x é a última a suportar o Python 3.5.

### Suporte do MariaDB
O Django agora suporta oficialmente o [MariaDB](https://mariadb.org/) 10.1 e superior.

### Suporte ASGI
O Django 3.0 começa a tornar o Django totalmente compatível com async, fornecendo suporte para execução como um aplicativo ASGI.

Isso é um acréscimo ao suporte WSGI existente. O Django pretende apoiar ambos no futuro próximo. Entretanto, os recursos assíncronos estarão disponíveis apenas para aplicativos executados em ASGI.

Observe que, como efeito colateral dessa mudança, o Django agora está ciente de loops de eventos assíncronos e irá bloquear o código de chamada marcado como "async unsafe" (assíncrono inseguro) - como operações ORM - de um contexto assíncrono. Se você estava usando o Django a partir de código assíncrono antes, isso pode ser acionado se você o fizer incorretamente. Se você tiver um erro de __SynchronousOnlyOperation__, examine atentamente o seu código e mova as operações do banco de dados para um thread filho síncrono.

### Restrições de exclusão no PostgreSQL
A nova classe __ExclusionConstraint__ permite adicionar restrições de exclusão no PostgreSQL. Restrições são adicionadas aos modelos usando a opção `Meta.constraints`.

### Expressões de filtro
As expressões que de saída como __BooleanField__ agora podem ser usadas diretamente nos filtros do __QuerySet__, sem precisar primeiro fazer anotações e depois filtrar a anotação.

### Enumerações para escolhas de um model field
Tipos de enumeração como __TextChoices__, __IntegerChoices__ e __Choices__ estão agora disponíveis como uma forma de definir `Field.choices`. Os tipos __TextChoices__ e __IntegerChoices__ são fornecidos para campos de texto e número inteiro. A classe __Choices__ permite definir uma enumeração compatível para outros tipos de dados concretos. Esses tipos de enumeração personalizados oferecem suporte a rótulos legíveis por humanos que podem ser traduzidos e acessados ​​por meio de uma propriedade na enumeração. Para mais detalhes veja [aqui](https://docs.djangoproject.com/en/3.0/ref/models/fields/#field-choices-enum-types).

Outras pequenas mudanças foram incluídas na nova versão, todas podem ser vistas [aqui](https://docs.djangoproject.com/en/3.0/releases/3.0/#minor-features).

_Esse dados foram consultados e traduzidos através da [nota oficial](https://docs.djangoproject.com/en/3.0/releases/3.0/) do django._

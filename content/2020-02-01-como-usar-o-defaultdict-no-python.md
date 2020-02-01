+++
title = "Como usar o defaultdict no Python"
date = 2020-02-01T01:00:00Z
draft = false
+++

Uma das coisas que torna o Python a ser uma linguagem de programação gostosa de se trabalhar é a utilização de dicionários (`dict`), objeto que representa uma estrutura de _chave/valor_.

Muitas vezes o uso excessivo de dicionários pode parecer confuso quando é preciso verificar se uma chave está contida nele. Vamos a um exemplo simples:

```python
dados = {
    'cores': [],
    'pessoas': [],
    'objetos': [],
}

novas_cores = ['Preto', 'Branco']
novas_pessoas = ['Taline', 'João', 'Maria']
novos_objetos = ['Caneta', 'Bola', 'Celular']

if 'cores' in dados:
    dados['cores'].extend(novas_cores)

if 'pessoas' in dados:
    dados['pessoas'].extend(novas_pessoas)

if 'objetos' in dados:
    dados['objetos'].extend(novos_objetos)
...

>>> print(dados)
{
    'cores': ['Preto', 'Branco'],
    'pessoas': ['Taline', 'João', 'Maria'],
    'objetos': ['Caneta', 'Bola', 'Celular']
}
```

O código acima pode parece extenso. Para adicionar valores em uma lista é verificado primeiro se no dicionário a chave existe, isso pode parecer confuso e acaba sendo repetitivo quando se tem muitos casos como este.

Uma solução para este "problema" é a utilização do dicionario `defaultdict`, uma subclasse de `dict` que já vem embutido no Python desde a versão 2.5, encontrado no módulo `collections`.
Vamos reescrever o exemplo acima utilizado defaultdict.

```python
from collections import defaultdict

dados = defaultdict(list)

novas_cores = ['Preto', 'Branco']
novas_pessoas = ['Taline', 'João', 'Maria']
novos_objetos = ['Caneta', 'Bola', 'Celular']

dados['cores'].extend(novas_cores)
dados['pessoas'].extend(novas_pessoas)
dados['objetos'].extend(novos_objetos)
...

>>> print(dados)
defaultdict(<class 'list'>, {'cores': ['Preto', 'Branco'], 'pessoas': ['Taline', 'João', 'Maria'], 'objetos': ['Caneta', 'Bola', 'Celular']})

>>> print(dict(dados))
{
    'cores': ['Preto', 'Branco'],
    'pessoas': ['Taline', 'João', 'Maria'],
    'objetos': ['Caneta', 'Bola', 'Celular']
}
```


A construção do `defaultdict` é bem simples, ele tem um único parâmetro chamado de _default_factory_, ele precisa ser uma função (`callable`). Se _default_factory_ não for informado ou for `None`, ele se comporta como um `dict` normal (ao acessar chaves que não existam acontece um `KeyError`)

Ao informar um parâmetro, o `defaultdict` vai criar uma chave automaticamente quando ela for acessada, se a chave não existir o _default_factory_ é chamado e cria um valor padrão, igual ao exemplo anterior, foi passado a função `list` e o dicionário cria uma nova lista vazia.

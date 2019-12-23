+++
title = "O que há de novo no python 3.8"
date = 2019-12-20T12:00:00Z
draft = false
+++

# Novidades no python 3.8!

O python 3.8.0 foi lançado 14/10/2019. Nessa versão surgem várias novidades. Entre elas estão, as expressões de atribuição, indicadores de parâmetros opcionais, novo especificador em f-strings, e muito mais.

Para mais detalhes sobre a nova versão do Python, acesse a [nota de lançamento](https://www.python.org/downloads/release/python-380/).

Abaixo vou mostrar alguns exemplos da nova versão que mais chamou a minha atenção.

## Expressão de atribuição (the walrus operator)

Python até então não possuía expressão de atribuição (_walrus_) como em outras linguagens. A sintaxe é usada através do operador `:=`.
Vamos a um exemplo:

Primeiro exemplo, sem o operador _walrus_:

```python
valor = input('Digite um valor: ')

if valor == 'ok':
    print(f'Você escreveu ok!')
```
Usando o operador _walrus_ com o exemplo anterior:

```python
if (valor := input('Digite um valor: ')) == 'ok':
    print(f'Você escreveu ok!')
```
Neste exemplo, quando o usuário digita um valor, o valor é atribuído a variável `valor`, depois o resultado é usado da expressão, verificando se o valor é igual a `'ok'`.

Particularmente acho mais difícil a leitura do código com o novo operador, especialmente para iniciantes em Python. Mas é possível fazer muitas coisas legais com ele (pouco código!). :D

## f-strings como debugging!

Ao utilizar `f-string` podemos adicionar o caracter `=` no final da variável ou expressão:

```python
preco = 200.20
nome = 'python'
print(f'{preco}')
print(f'{nome}')
print(f'{preco=}')
print(f'{nome=}')

>>> 200.2
>>> python
>>> preco=200.2
>>> nome='python'
```

Podemos ver que ao imprimir a variável com `=` é mostrado `variavel=valor`, isso ajuda na hora de depurar algum código.

Também é possível usar o operador _walrus_ com `f-string` de um jeito bem simples:

```python
print(f'Estou escolhendo o valor {(valor := 1 + 1)} e o dobro dele é {valor*2}')

>>> Estou usando o valor 2 e o dobro dele é 4
```

## Argumentos apenas de posição (Positional-Only Arguments)

No Python 3.8 se for fazer `help(int)`, por exemplo, é retornado a seguinte informação:

```
class int(object)
 |  int([x]) -> integer
 |  int(x, base=10) -> integer
 |
 |  Convert a number or string to an integer, or return 0 if no arguments
 |  ...
 |
 |  __abs__(self, /)
 |      abs(self)
 |
 |  __add__(self, value, /)
 |      Return self+value.
 |
 |  __and__(self, value, /)
 |      Return self&value.
 | ...
```

Existe uma `/` no final de cada método. O'Que ele indica é que, todos os parâmetros antes dele são apenas posicionais. Podemos ver isso em um exemplo:

```python
def faz_algo(a, b, /):
    print(f'Fazendo algo com {a} e {b}...')
```

Podemos usar a função normalmente:

```python
faz_algo(1, 2)
>>> Fazendo algo com 1 e 2...

faz_algo(1, b=2)
>>> TypeError: faz_algo() got some positional-only arguments passed as keyword arguments: 'b'
```

Ao informar algum parâmetro de forma nomeada acontece um `TypeError`. O próprio erro diz que a chamada de `faz_algo` obteve alguns argumentos **apenas de posição** passados como argumentos de palavra-chave.

Podemos especificar que somente um parâmetro da função é somente posicional:

```python
def faz_algo(a, /, b):
    print(f'Fazendo algo com {a} e {b}...')

faz_algo(1, b=2)

>>> Fazendo algo com 1 e 2...
```

Também é possível especificar para uma função que os parâmetros devem ser apenas nomeados usando o `*`, com isso todos os parâmetros que forem passados **depois** do `*` serão somente nomeados.

```python
def faz_algo(*, a, b):
    print(f'Fazendo algo com {a} e {b}...')

faz_algo(a=1, b=2)
>>> Fazendo algo com 1 e 2...

faz_algo(1, b=2)
>>> TypeError: faz_algo() takes 0 positional arguments but 1 positional argument (and 1 keyword-only argument) were given
```

Antes do python 3.8 era difícil dizer como determinado código deve ser chamado, geralmente era usado de forma "certa" em código interno. Ao meu ver, usar `/` ou `*`, temos o controle de como determinado código deve se comportar, isso traz uma legibilidade a quem usa, onde um função/método vai poder ser escrito de um único jeito, seguindo a própria assinatura informada e evitando alguns erros.

Muitas coisas foram adicionadas no Python 3.8, todas podem ser vistas na [documentação](https://docs.python.org/3.8/whatsnew/3.8.html), vale a pena ver.

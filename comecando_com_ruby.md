# Começando com Ruby
```ruby
puts "Hello Tutorial"
```
## Variáveis em ruby

Ruby é uma linguagem de tipagem dinâmica e fortemente tipada, isto é variaveis podem ser declaradas de maneira dinâmica não sendo necessário declarar o tipo da mesma antes de atribuir o valor e a mesma pode ser atribuida para outro tipo de variavel a qualquer momento no código, ao mesmo tempo o ruby tem tipagem forte, assim o ruby não irá converter automaticamente um tipo pra o outro.

O código a seguir retornaria um erro por exemplo:
```ruby
num = 123
puts "Isso não irá concatenar com um número" + num
```

O código acima iria retornar um TypeError dizendo que não é possível fazer uma conversão implicita de Fixnum com string, para corrigirmos isso podemos converter um número para string com o método **'to_s'**:

```ruby
num = 123
puts "Isso concatena com um número " + num.to_s
```

Aliás, esse nem é o melhor jeito para juntar strings com variaveis em ruby, o ruby possui suporte a interpolação de strings, isso quer dizer que poderiamos escrever:
```ruby
num = 123
puts "Isso concatena com um número #{num}"  
```
Tudo em ruby são objetos, até uma classe é um tipo de objeto e isso se dá também com as variáveis em ruby, não há tipos primitivos como em java ou C#  e em outras linguagens (int, float e boolean são exemplos de tipos primitivos), todas variáveis em ruby também são objetos.

#### Números
```ruby
#Números inteiros
1.class #=> Fixnum
num = 2
num.class #=> FixNum

#Números em ponto flutuante

3.6.class #=> Float
num = 200.2
num.class #=> Float


```


# Começando com Ruby
```ruby
puts "Hello Tutorial"
```
## Declarando Variáveis em ruby

Ruby é uma linguagem de tipagem dinâmica, assim as variáveis não pecisam ser declaradas, o ruby já irá saber qual será o tipo da variável no momento de atribuição da mesma, conforme o exemplo a seguir:

```ruby
num = 123
texto = "Hello Ruby"
array_legal = [1,2,3,true,"Que legal"]
```
Por ser de tipagem dinâmica uma mesma variável pode ser atribuida para outro tipo de variável a qualquer momento no código.

```ruby
a = 123 # Aqui "a" é um número
a = "Hello Cebola" #Aqui "a" virou uma string
a = [1,2] #Agora "a" é um array
```
O Ruby também permite que você declare várias variáveis em uma única linha, exemplo:
```ruby
a,b,c = 1,2,3 # a = 1, b = 2, c = 3
```
Mesmo tendo tipagem dinâmica o ruby tem tipagem forte, assim ele não irá converter automaticamente um tipo pra o outro.

Pro exemplo, o código a seguir retornaria um erro:
```ruby
num = 123
puts "Isso não irá concatenar com um número" + num
```

O código acima iria retornar um TypeError dizendo que não é possível fazer uma conversão implicita de Fixnum com String, para corrigirmos isso podemos converter um número para string com o método **'to_s'**:

```ruby
num = 123
puts "Isso concatena com um número " + num.to_s
```

Falando dos tipos de variáveis em relação ao escopo, podemos ter variáveis globais, locais, de instância e de classes e além das variáveis também temos as constantes.

```ruby
$v = "Variáveis globais começam com $"
v = "Variáveis locais começam com uma letra minúscula ou _"
@v = "Variáveis de instância começam com @"
@@v = "Variáveis de classe começam com @@"
CONSTANTE = "Constantes começam com uma letra maiuscula e por convenção tem todas as letras em maiúsculo "
```

### Tipos de variáveis

Tudo em ruby são objetos, até uma classe é um tipo de objeto e isso se dá também com as variáveis em ruby, não há tipos primitivos como em Java, C# (int, float e boolean são exemplos de tipos primitivos), todas variáveis em ruby também são objetos.

#### Números
```ruby
#Números inteiros
1.class #=> Fixnum
num = 2
num.class #=> FixNum
0xff.class #=> FixNum (Representação em hexadecimal)
0b1011.class #=> FixNum (Representação em binário)
0377.class #=> FixNum (Representação em octal)

#Números em ponto flutuante
3.6.class #=> Float
num = 200.2
num.class #=> Float
#pontos flutuantes com notação cientifica
puts 1.0e6 #=> 1000000.0
4e+20 * 2 #=> 8.0e+20
4E20.to_i #=> 400000000000000000000
```

Sendo objetos os tipos em ruby também possuem métodos e atributos, no exemplo acima o metodo 'to_i' é invocado de um Float e retorna um inteiro.

#### Strings

Nos exemplos anteriores já foi mostrado a você alguns exemplos com strings, em um exemplo vimos como podemos fazer a concatenação em ruby, aliás, aquele nem é o melhor jeito para juntar strings com variaveis em ruby, o ruby possui suporte a interpolação de strings, isso quer dizer que poderiamos escrever:
```ruby
num = 123
puts "Isso concatena com um número #{num}"  
```

O codigo acima irá validar o que está dentro de #{} e retornar para a string, além de variáveis também é possível colocar dentro dele funções que retornem valores.

Strings podem ser declaradas de várias maneiras:
```ruby
c = 'Sem interpolação'
e = "#{interpolação}, e caracteres de escape \n"
b = %q(sem interpolação)
o = %Q(suporta interpolação e caracteres de escape)
l = %(suporta interpolação e caracteres de escape)
a = String.new #Retorna uma string vazia ""
```
O \n no segundo exemplo representa a quebra de linha em um texto, o uso da % pode ser customizado para outros delimitadores, por exemplo:
```ruby

s = %{texto}
e = %[texto]
m = %$texto$
```

Note que assim que você escolhe um delimitador se for necessário representá-lo dentro da string ele deverá ser escapado:

```ruby
s = %{texto e com o \} dentro}
e = %[texto e com o \] dentro]
m = %$texto e com o \$ dentro$
```

### Symbols

São parecidos com strings, mas são objetos que são usados para representar algum nome ou chave e ao contrário de string um objeto symbol com o mesmo valor é o mesmo objeto em toda execução do programa, para se criar um symbol apenas coloque ':' antes do nome do symbol, exemplo:

```ruby
#declarando symbols
s = :symbol
s2 = :"symbol com espaços"

#Diferente das strings um symbol sempre é a representação de um mesmo objeto

:symbol.object_id == :symbol.object_id #=> true
"string".object_id == "string".object_id #=> false
```

Mais a frente veremos algumas utilizações com symbols.


### Arrays

Os arrays em ruby são coleções que suportam qualquer tipo de objeto dentro deles, é possível ter em um mesmo array uma String, um Fixnum, valores booleanos, outros arrays, enfim qualquer outro objeto.

```ruby
array_legal = [0,"texto",[0,1],true]
```

Assim como as strings os arrays podem ser definidos de várias formas:

```ruby
array_legal = [0,1,2]

array_mais_legal = %w{a b c d} #=> ["a", "b", "c", "d"]

array_ok = Array.new([1,2,3]) #=> [1, 2, 3]

array_repetido = Array.new(3, "knock") #=> ["knock", "knock", "knock"]

```

Os índices em um array sempre começam em 0, para acessar ou atribuir os itens de um array podemos utilizar os índices ou alguns métodos:

```ruby
array_sucesso = [1,2,10,20]

array_sucesso.first # Retorna o primeiro elemento no caso o 1
array_sucesso[0] # Retorna o elemento com o índice 0 no caso o 1
array_sucesso[2] # Retorna o elemento com o índice 2 no caso o 10
array_sucesso.last # Retorna o último elemento no caso o 20

# Quando passamos um índice negativo será contado
# os itens das últimas posições para as primeiras
array_sucesso[-1] # Retorna o último elemento no caso o 20
array_sucesso[-2] # Retorna o penúltimo elemento no caso o 10

#Para atribuir passamos o índice e o valor
array_sucesso[0] = 90
array_sucesso.inspect #=> [90,2,10,20]

#Para adicionar novos itens
array_sucesso << 2
array_sucesso.inspect #=> [90,2,10,20,2]
```

Os arrays possuem diversos métodos que nos possibilitam filtrar, pesquisar ou alterar itens, segue alguns deles:

```ruby
array_sucesso = [1,2,10,20,30]

##select##
# Retorna um novo array com todos os elementos
# que correspondam com a condição lógica passada em um bloco
array_sucesso.select{|e| e < 5} #=> [1,2]
array_sucesso.select{|e| e.even?} #=> [2,10,20,30]

##reject##
# Retorna um novo array com todos os elementos
# que  não correspondam com a condição lógica passada em um bloco
array_sucesso.reject{|e| e < 5} #=> [10, 20, 30]
array_sucesso.reject{|e| e.even?} #=> [1]

##map##
# Retorna um novo Array transformado de acordo com um bloco de código

# Nesse exemplo retorna um novo array somando 2
# em todos os itens do array dado
array_sucesso.map{|e| e + 2} #=> [3, 4, 12, 22, 32]
```

Além desses existem vários outros métodos disponiveis, recomendo a leitura da Classe [Array]  para se familiarizar com eles.

### Hash

Os hashes são coleções parecidas com arrays, mas que possuem chaves como índice ao invés de apenas números. Os índices podem ser qualquer tipo de objeto. 

```ruby
#Pode ser criado por {}
omelete = {
    "ovos" => 2,
    "queijo" => 1,
    "tomate" => 1
    "cebola" => 0
}
#No caso de symbols como chave o uso do rocket operator('=>') é opcional 
#É possível simplesmente colocar o ':' do outro lado:

omelete = {
    ovos: 2,
    queijo: 1,
    tomate: 1,
    cebola: 0
} 

#Ainda é possível criar passando um array,nesse caso o primeiro valor será a chave, o segundo o valor, o terceiro a chave e assim por diante.
omelete = Hash[:ovos, 2,:queijo, 1,:tomate,1,:cebola,0]

#Ou ainda é possível adicionar um Hash vazio e adicionar cada dado
omelete = Hash.new
omelete[:ovos] = 2
omelete[:queijo] = 1
omelete[:tomate] = 1
omelete[:cebola] = 0
```
No caso de criarmos um novo hash pelo metodo new também podemos passar um bloco de código que será executado toda vez que uma chave que ainda não existe no hash for chamada e recebe como parametro o proprio hash e a chave que não existe.
No exemplo a seguir instanciamos um novo hash vazio em que caso seja chamado uma chave :cebola que ainda não existe ele retornará "sem cebola". 

```ruby
omelete_sem_cebola = Hash.new{|hash, key| "sem cebola" if key = :cebola}

#Ou ainda podemos usar ele ainda para retornar um valor padrão
ideias = Hash.new{|hash, key| "sem ideias sobre isso"}
ideias["O que você acha de um omelete sem cebola?"] #=> "sem ideias sobre isso"
```
Ou podemos fazer alguma operação e guardar o valor, no exemplo a seguir vamos fazer um hash que retorna o fatorial de cada número, ou seja, cada chave irá possuir o seu fatorial como valor que será calculado na primeira vez que ele for chamado.

```ruby
fat = Hash.new do |hash,key|
    if [0,1].include? key.to_i
        hash[key] = 1
    else
        hash[key] = (1..key.to_i).reduce(:*)
    end
end

fat[5] #=> 120
fat[3] #=> 6
```
Perceba que o calculo só será feito da primeira vez, nas próximas o valor ja estará guardado no hash.



Recomendo uma leitura da classe [Hash] para ver mais sobre as suas possibilidades.

## Estruturas de decisão 

No exemplo anterior já usamos a estrutura de decisão mais comum com if e um else, vamos ver agora algumas outras possibilidades que o ruby permite.

Alguns dos operadores lógicos:
* **&&** -> Operador 'e'
* **||** -> operador 'ou'
* **!** -> negação

### If

Supondo que temos que validar que duas variáveis são iguais para executar uma ação especifica podemos construir o if da maneira clássica:

```ruby
omelete1 = ['queijo','ovos']
omelete2 = ['queijo', 'ovos']

if omelete1 == omelete2
    puts "Justo"
end
```

Porém em casos que executamos apenas uma ação apos o if podemos usar o if em apenas uma linha:

```ruby
omelete1 = ['queijo','ovos']
omelete2 = ['queijo', 'ovos']

puts "Justo" if omelete1 == omelete2
```

Caso queremos verificar que algo algo é diferente podemos usar o operador booleano "!=" ou negar toda a expressão lógica.

```ruby
omelete1 = ['queijo','ovos']
omelete2 = ['queijo', 'ovos','cebola']

#If normal
if omelete1 == omelete2
    puts "Justo"
end
#If em uma linha
puts "O meu omelete é diferente" if omelete1 != omelete2
puts "O meu omelete é diferente" if !(omelete1 == omelete2)
```

### Unless

Porém em casos em que usamos uma negação no if podemos alternativamente usar o unless.

```ruby
omelete1 = ['queijo','ovos']
omelete2 = ['queijo', 'ovos','cebola']

puts "O meu omelete é diferente" unless omelete1 == omelete2
```

No entanto há situações em que o unless não é recomendado:

* A estrutura de decisão possui um else
* A estrutura de decisão possui combinações lógicas com **&&**, **||** ou **!**

Em ambos os casos o unless não é indicado devido ao fato de poder deixar confuso o resultado da expressão lógica.

### If com else

Em caso de queremos validar as duas possibilidades em uma decisão podemos usar a estrutura clássica do if e else...
```ruby
if 1 == 1
    puts "Ainda bem"
else
    puts "Deu ruim"
end
```
...ou em uma linha:

```ruby
if 1 == 1 then puts "Ainda bem" else puts "Deu ruim" end
if 1 == 1; puts "Ainda bem" else puts "Deu ruim" end
```

Perceba que ao escrever em uma linha a palavra reservada **'then'** ou o **';'** é obrigatório.

### If com else if

Caso queremos fazer uma segunda validação podemos utilizar o elsif

```ruby
pedido = ['omelete','biscoito','suco'].sample #Pega aleatoriamente um item do array
if pedido == 'biscoito'
    puts "Tá ai o biscoito"
elsif pedido == 'suco'
    puts "Tá aí o suco"
else
    puts "Não tem biscoito!!!!!!!!!!"
end
```

##Atribuindo o resultado de uma operação lógica a uma variável
Em todos os casos podemos pegar o resultado de um if e armazenalo em uma variável, o resultado sempre será a ultima linha do bloco em que a operação lógica for verdadeira.
```ruby
def tem_biscoito?
    [true,false].sample
end

resposta = if tem_biscoito?
        "Tá ai o biscoito" #Retorna isso se a operação lógica for verdadeira
    else
        "Não tem biscoito!!!!!!!!!!" #Retorna isso se a operação lógica for falsa
    end
    
puts resposta #=> "Tá ai o biscoito" ou "Não tem biscoito!!!!!!!!!!"
```


### Case

É possível aninhar quantos elsif for necessários para validar todas as opções possíveis mas nesses casos é recomendado usar o case:

```ruby
pedido = ['omelete','biscoito','suco',"cebola"].sample #Pega aleatoriamente um item do array

case pedido
when 'omelete'
    puts "Pegando o Omelete"
when 'biscoito'
    puts "Pegando o Biscoito"
when 'suco'
    puts "Pegando o suco de uva"
else 
    puts "Não temos isso"
end
```
 Assim como o if também podemos armazenar o resultado do case:
 
 ```ruby
pedido = ['omelete','biscoito','suco',"cebola"].sample #Pega aleatoriamente um item do array

resposta = case pedido
when 'omelete'
    "Pegando o Omelete"
when 'biscoito'
    "Pegando o Biscoito"
when 'suco'
    "Pegando o suco de uva"
else 
    "Não temos isso"
end

puts resposta
```

Alternativamente também podemos usar o then:

 ```ruby
pedido = ['omelete','biscoito','suco',"cebola"].sample #Pega aleatoriamente um item do array

resposta = case pedido
when 'omelete' then "Pegando o Omelete"
when 'biscoito' then "Pegando o Biscoito"
when 'suco' then "Pegando o suco de uva"
else "Não temos isso"
end

puts resposta
```

### Estruturas de repetição

O ruby suporta todas as estruturas de repetição comuns em outras linguagens.

 ```ruby
# While
cont = 0
while (cont <= 10) do 
    puts cont
    cont += 1
end

# Do While
cont = 0
begin 
  puts cont
  cont+=1
end while (cont <= 10)

# Until
count = 0
until (count >= 10) do 
    puts count
    count += 1
end

# Do Until
count = 0
begin 
  puts count
  count+=1
end until (count >= 10)

#For Loop
for i in 0..10
    puts i
end
```

Poderiamos assim percorrer um array da mesma maneira que fazemos em outras linguagens:

 ```ruby
opcoes = ['omelete','biscoito','suco',"cebola"]

#Por indice
for i in (0..opcoes.size-1)
    puts opcoes[i]
end

#Por item (Estilo o for each presente em algumas linguagens)
for opcao in opcoes
    puts opcao
end
```

Apesar de ser possível a pratica acima nao é maneira mais idiomática no ruby de resolver esse problema, para esse caso temos o método each:

 ```ruby
opcoes = ['omelete','biscoito','suco',"cebola"]

opcoes.each do |opcao|
    puts opcao
end
```

Mesmo em casos que não desejamos percorrer um array e sim executar uma mesma ação durante várias temos várias alternativas ao for.

 ```ruby
10.times{ puts "Hello"}

#caso precise do índice
(1..10).each_with_index {|num,i| puts "O índice de #{num} é #{i}"}
```

[Array]: http://docs.ruby-lang.org/en/2.0.0/Array.html
[Hash]: https://ruby-doc.org/core-2.3.0/Hash.html

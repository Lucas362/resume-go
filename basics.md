# Go

Go é uma linguagem de programação open-source desenvolvida pela Google. É estaticamente tipada, possui garbage collector e suporta programação concorrente, utilizando goroutine e channels.

## Instalando

Acesse https://golang.org/dl/ e baixe a versão compatível com seu S.O.

Após instalado digite o comando a seguir em seu terminal para verificar se a instalação ocorreu e qual versão foi instalada:
```
go version
```

Você deverá ter uma resposta como:
```
go version go1.12.6 linux/amd64
```

## Executando um programa

Para executar um programa em go, no terminal, acesse o diretório de seu arquivo e digite o seguinte comando:
```
go run <nome_do_arquivo>
```

Exemplo de programa em GO:

```go
package Main

import "fmt"

func main() {
    fmt.Println("Hello World")
}
```

Executando o programa (aqui vamos chamar o programa de hello.go):
```
go run hello.go

Saída: Hello World
```

## Tipos de dados

* `numéricos`: int8, int16, int32, int64, uint8, uint16, uint32, uint64, float32, float64, complex64, complex128;
* `Strings`: Concatenação de vários caracteres, possui métodos como concatenação, extração de substring, etc;
* `Boolean`: true ou false.

## Variáveis

Go é tipado estaticamente. Ex:
```go
var <variable_name> <type>
```

É possível inicializar a variável ao criar:
```go
var <variable_name> <type> = <value>

// Não é necessário colocar o tipo neste caso, o go consegue abstrair a partir do <value>
var <variable_name> = <value>

var <variable_name1>, <variable_name2>, <variable_name3> = <value1>, <value2>, <value3>
```

Além disto, o Go permite a criação de variáveis omitindo a palavra `var`:
```go
<variable_name> := <value>
```

Esta sintaxe não pode ser utilizada para atribuir valor a uma variável já criada.

Exemplo:
```go
package main
import "fmt"

func main() {
	var x int
	x = 3

	var y int = 20

	var z = 50

	w := 70

	fmt.Println("x:", x, "- y:", y, "- z:", z, "- w:", w)
}

Saída: x: 3 - y: 20 - z: 50 - w: 70
```

## Contantes

Para criar uma constante utilize a palavra reservada `const`. Ex:
```go
package main
import "fmt"

func main() {
    const b = 10
    fmt.Println(b)
}

Saída: 10
```

## If else

Sintaxe:
```go
if condition {
    // code
} else if condition{
    // code
} else {
    // code
}
```

Ex:
```go
package main
import "fmt"

func main() {
	var x = 100
	if x < 10 {
		fmt.Println("Menor que 10")
	} else if x >= 10 && x <= 99 {
		fmt.Println("Entre 10 e 99")
	} else {
		fmt.Println("Maior que 99")
	}
}

Saída: Maior que 99
```

## Switch

Sintaxe:
```go
switch expression {
    case value_1:
        // code
    case value_2:
        // code
    case value_n:
        // code
    default:
        // code
}
```

Ex:
```go
package main
import "fmt"

func main() {
	a,b := 2,1

	switch a+b {
		case 2:
			fmt.Println("Resultado == 2")
		case 3:
			fmt.Println("Resultado == 3")
		case 5:
			fmt.Println("Resultado == 5")
		default:
			fmt.Println("Outro valor")
	}
}

Saída: Resultado == 3
```

## Loops

Go suporta somente `for` (diferente das outras linguagens que geralmente aceitam for, while e do while). Sintaxe:

```go
for expressao_inicial; expressao_avaliacao; iteracao {
    // code
}
```
Ou, de acordo com a documentação "For is Go's 'while'", sintaxe:
```go
for expression {
    // code
}
```
Ex:
```go
package main
import "fmt"

func main() {
	var sum int
	for sum = 1; sum <= 5; sum++ {
		fmt.Println(sum)
	}
}

Saída: 1
2
3
4
5
```

```go
package main
import "fmt"

func main() {
	sum := 0
	for sum < 5 {
		sum++
		fmt.Println(sum)
	}
}

Saída: 1
2
3
4
5
```

## Arrays

Arrays têm tamanho fixo e só podem armazenar dados de um mesmo tipo. Sintaxe:
```go
var arrayname [size] type
```

É possível atribuir valores a um array em sua declaração. Sintaxe:
```go
arrayname := [size] type {value_0, value_1, ..., value_size-1}

// Não é nessário dizer o tamanho, o Go consegue abstrair a partir da quantidade de elementos
arrayname := [...] type {value_0, value_1, ..., value_size-1}
```

Para atribuir valor a uma posiçao de um array use:
```go
arrayname[index] = value
```

Para saber o tamanho de um array use:
```go
len(arrayname)
```

Exemplo: 
```go
package main
import "fmt"

func main() {
	var numbers [3] string
	numbers[0] = "um"
	numbers[1] = "dois"
	numbers[2] = "três"

	numbers2 := [3] string {"quatro", "cinco", "seis"}

	numbers3 := [...] string {"sete", "oito", "nove"}

	fmt.Println(numbers)
	fmt.Println(numbers2)
	fmt.Println(numbers3)
	fmt.Println(numbers[0])
}

Saída: [um dois três]
[quatro cinco seis]
[sete oito nove]
um
```

### Slice

Representa uma parte do array, `os valores são ponteiros para o array original, logo, ao alterar o slice, o array original também será alterado`. Sintaxe:
```go
var slice_name [] type = array_name[start:end]
```

Ex:
```go
package main
import "fmt"

func main() {
	a := [5] string {"um", "dois", "três", "quatro", "cinco"}
	
	var b [] string = a[1:4]

	fmt.Println("Sem alteração:", a, b)

	b[0] = "dez"

	fmt.Println("Com alteração:", a, b)
}

Saída: Sem alteração: [um dois três quatro cinco] [dois três quatro]
Com alteração: [um dez três quatro cinco] [dez três quatro]
```
Alguns métodos do slice:

* `len(slice_name)`: Tamanho do slice;
* `append(slice_namr, value_name1, ...)`: Adiciona um item ao fim do slice (substitui no original caso o slice não termine na última posição do array original).
* `append(slice_name1, slice_name2)`: Adiciona slice_name2 ao slice_name1.

## Funções

Sintaxe:
```go
func function_name(parameter_1 type, ..., parameter_2 type) return_type {
	// code
}
```

Ex: 
```go

```
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
package main

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

## Constantes

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
package main
import "fmt"

func calc(num1 int, num2 int) (int, int) {
	sum := num1 + num2
	diff := num1 - num2
	return sum, diff
}

func main() {
	x, y := 15, 10

	sum, diff := calc(x, y)
	fmt.Println("Sum", sum)
	fmt.Println("Diff", diff)
}

Saída: Sum 25
Diff 5
```

## Pacotes

Permite a divisão do código em diversos arquivos. Sintaxe:
```go
import package_name
```

## Adiamentos

É possível adiar a execução de uma chamada de função através do uso do `defer`. Sintaxe:
```go
defer function()
```
Ex:
```go
package main
import "fmt"

func exemplo() {
	fmt.Println("Dentro de exemplo()")
}

func main() {
	defer exemplo()
	fmt.Println("Dentro de main()")
}

Saída: Dentro de main()
Dentro de exemplo()
```

## Ponteiros

Go trabalha com ponteiros da mesma maneira que a linguagem C (ao enos do ponto de vista sintático). Utilizando `&` e `*`. Ex:
```go
package main
import "fmt"

func main() {
	a := 20

	var b *int = &a

	fmt.Println("Endereço de a:", &a)
	fmt.Println("Valor de a:", a)

	fmt.Println("Endereço contido em b:", b)
	fmt.Println("Valor contido em b:", *b)

	*b = *b+1

	fmt.Println("Valor atualizado contido em b:", *b)
	fmt.Println("Valor atualizado de a", a)
}

Saída: Endereço de a: 0xc0000140c0
Valor de a: 20
Endereço contido em b: 0xc0000140c0
Valor contido em b: 20
Valor atualizado contido em b: 21
Valor atualizado de a 21
```

## Structures

Conjunto de dados de tipos heterogêneos. Sintaxe:
```go
type structname struct {
	variable_1 variable_1_type
	variable_2 variable_2_type
	variable_n variable_n_type
}
```
Ex:
```go
type pessoa struct {
	nome string
	endereco string
	idade int
}
```

Para declarar uma variável do tipo da struct a sintaxe segue o padrão da declaração comum:
```go
var variable_name struct_name
```
Ex:
```go
var pessoa1 pessoa
```

Para setar valores de uma struct a sintaxe é:
```go
pessoa1.nome = "joão"
pessoa1.endereco = "rua tal bairro algum cidade top"
pessoa1.idade = 50
```

Também é possível criar uma variável com valores iniciais setados. Ex:
```go
pessoa2 := pessoa{"judiscleidson", "lugar nenhum", 25}
```

Exemplo total:
```go
package main
import "fmt"

type pessoa struct {
	nome string
	endereco string
	idade int
}

func main() {
	var pessoa1 pessoa
	pessoa1.nome = "joão"
	pessoa1.endereco = "rua tal bairro algum cidade top"
	pessoa1.idade = 50

	pessoa2 := pessoa{"judiscleidson", "lugar nenhum", 25}

	fmt.Println(pessoa1.nome)
	fmt.Println(pessoa2.nome)
}

Saída: joão
judiscleidson
```

## Métodos

Apesar de Go não ser uma linguagem orientada a objetos, é possível utilizar métodos associados aos tipos de dados utilizando `métodos`. sintaxe:
```go
func(variable variable_type) methodName(paramether1 paramether_1_type, paramethern paramether_n_type){}
```
Ex:
```go
package main
import "fmt"

type pessoa struct {
	nome string
	endereco string
	idade int
}

func(p pessoa) display(nome string, idade int) {
	fmt.Println(p.endereco, nome, idade)
}

func main() {
	pessoa1 := pessoa{"pessoa 1", "lugar nenhum", 10}
	pessoa2 := pessoa{"pessoa 2", "lugar nenhum", 20}

	pessoa1.display(pessoa1.nome, pessoa1.idade)
	pessoa2.display(pessoa2.nome, pessoa2.idade)
}
```

## Goroutines
`Goroutines` são funções que rodam de forma concorrente com outras funções. O programa não irá esperar pelo fim da execução de uma `goroutine`, diferente do que acontece com as outras funções. Sintaxe:
```go
go function_name(paramether_1, paramether_n)
```
Como dito anteriormente, o programa não espera pelo fim da execução da `goroutine`, como pode ser visto pelo exemplo a seguir:
```go
package main
import "fmt"

func display() {
    fmt.Println("Na display")

}

func main() {
    go display()

    for i:=0; i<5; i++ {
        fmt.Println("Na main")
    }
}

Saída: Na main
Na main
Na main
Na main
Na main
```
Adicionando uma pausa para a execução de `display` acontecer:
```go
package main
import "fmt"
import "time"

func display() {
    for i:=0; i<5; i++ {
        time.Sleep(1*time.Second)
        fmt.Println("Na display")
    }
}

func main() {
    go display()

    for i:=0; i<5; i++ {
        time.Sleep(2*time.Second)
        fmt.Println("Na main")
    }
}

Saída: Na display
Na main
Na display
Na display
Na main
Na display
Na display
Na main
Na main
Na main
```

## Channels

`Channel` é um caminho pelo qual as funções comunicam umas com as outras. Sintaxe:
```go
channel_variable := make(chan type)
```

Para enviar dados para um `channel` esta é a sintaxe:
```go
channel_variable <- variable_name>
```

Para receber dados de um `channel` esta é a sintaxe:
```go
variable_name := <- channel_variable
```

É possível fechar o `channel` indicando que a comunicação entre as funções não se comunicaram mais através dele. Sintaxe:
```go
close(channel_name)
```

Também é possível receber o status de um `channel`, ou seja, se ele foi fechado ou não no momento de receber o valor. Sintaxe:
```go
variable_name, status := <- channel_variable
```

Exemplo:
```go
package main
import "fmt"
import "time"

func add_to_channel(ch chan int) {
	fmt.Println("Send data")
	for i:=0; i<10; i++ {
		ch <- i
	}
	close(ch)
}

func fetch_from_channel(ch chan int) {
	fmt.Println("Read data")
	for {
		x, flag := <- ch
		if flag == true {
			fmt.Println(x)
		} else {
			fmt.Println("Empty channel")
			break
		}
	}
}

func main() {
	ch := make(chan int)

	go add_to_channel(ch)
	go fetch_from_channel(ch)

	time.Sleep(5 * time.Second)
	fmt.Println("Inside main()")
}

Saída: Envia dado
Lê dado
0
1
2
3
4
5
6
7
8
9
Channel fechado
Na main()
```

## Select
Funciona como um `switch` para `channels`. Ele espera até a inserção de dados em algum dos `channels`. Ex:
```go
package main
import "fmt"
import "time"

func data1(ch chan string) {
	time.Sleep(4 * time.Second)
	ch <- "from data1()"
}

func data2(ch chan string) {
	time.Sleep(2 * time.Second)
	ch <- "from data2()"
}

func main() {
	chan1 := make(chan string)
	chan2 := make(chan string)

	go data1(chan1)
	go data2(chan2)

	select {
	case x := <- chan1:
		fmt.Println(x)
	case y := <- chan2:
		fmt.Println(y)
	}
}

Saída: from data2()
```

Também é possível utilizar o `default` no select, que executa sem esperar algum `channel` receber valor. Ex:
```go
package main
import "fmt"
import "time"

func data1(ch chan string) {
	time.Sleep(4 * time.Second)
	ch <- "from data1()"
}

func data2(ch chan string) {
	time.Sleep(2 * time.Second)
	ch <- "from data2()"
}

func main() {
	chan1 := make(chan string)
	chan2 := make(chan string)

	go data1(chan1)
	go data2(chan2)

	select {
	case x := <- chan1:
		fmt.Println(x)
	case y := <- chan2:
		fmt.Println(y)
	default:
		fmt.Println("Default case")
	}
}

Saída: Default case
```

## Mutex
É a forma diminuída de mutual exclusion. É utilizado quando não se quer permitir a um recurso ser acessado por múltiplas subrotinas ao mesmo tempo. O `mutex` possui os métodos `lock` e `unlock`. Caso mutex não seja utilizado:
```go
package main
import "fmt"
import "time"
import "strconv"
import "math/rand"

var count = 0

func process(n int) {
	for i:=0; i<10; i++ {
		time.Sleep(time.Duration(rand.Int31n(2)) * time.Second)
		temp := count
		temp++
		time.Sleep(time.Duration(rand.Int31n(2)) * time.Second)
		count = temp
	}
	fmt.Println("Count after i="+strconv.Itoa(n)+" Count:", strconv.Itoa(count))
}

func main() {
	for i:=1; i<4; i++ {
		go process(i)
	}

	time.Sleep(25 * time.Second)
	fmt.Println("Final Count:", count)
}

Saída: Count after i=3 Count: 10
Count after i=1 Count: 14
Count after i=2 Count: 15
Final Count: 15

Obs: a saída varia de execução para execução
```

Com `mutex`:
```go
package main
import "fmt"
import "time"
import "sync"
import "strconv"
import "math/rand"

var mu sync.Mutex
var count = 0

func process(n int) {
	for i:=0; i<10; i++ {
		time.Sleep(time.Duration(rand.Int31n(2)) * time.Second)
		mu.Lock()
		temp := count
		temp++
		time.Sleep(time.Duration(rand.Int31n(2)) * time.Second)
		count = temp
		mu.Unlock()
	}
	fmt.Println("Count after i="+strconv.Itoa(n)+" Count:", strconv.Itoa(count))
}

func main() {
	for i:=1; i<4; i++ {
		go process(i)
	}

	time.Sleep(25 * time.Second)
	fmt.Println("Final Count:", count)
}

Saída: Count after i=3 Count: 21
Count after i=1 Count: 29
Count after i=2 Count: 30
Final Count: 30
```

Esta diferença se pelo fato de, sem a utilização do `mutex`, a variável é acessada e sobrescrita de forma desordenada, o que cria a incoerência no valor.

## Tratamento de erros
O tratamento de erros no Go é bastante simples. Ex:
```go
package main
import "fmt"
import "os"

func fileopen(name string) {
	f, er := os.Open(name)

	if er != nil {
		fmt.Println(er)
		return
	} else {
		fmt.Println("file opened", f.Name())
	}
}

func main() {
	fileopen("invalid.txt")
}

Saída: open invalid.txt: no such file or directory
```

### Erros customizados
Sobrescreve os erros padrões (e cria novos, caso necessário). Ex:
```go
package main
import "fmt"
import "os"
import "errors"

func fileopen(name string) (string, error) {
	f, er := os.Open(name)

	if er != nil {
		return "", errors.New("Custom error message: File name is wrong")
	} else {
		return f.Name(), nil
	}
}

func main() {
	filename, error := fileopen("invalid.txt")
	if error != nil {
		fmt.Println(error)
	} else {
		fmt.Println("file opened", filename)
	}
}

Saída: Custom error message: File name is wrong
```
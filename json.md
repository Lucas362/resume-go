# Json
Por ser uma linguagem fortemente tipada (todas as variáveis tem um tipo específico desde de sua criação até o fim da execução), realizar um parse de json é relativamente problemático. Aqui serão mostradas duas formas de tratar json, a forma estática e a forma dinâmica.

## Json estático
Com json estático, estamos nos referindo a json onde todas as chaves e seus tipos de valor correspondentes são conhecidos e não vão mudar. 

### Structs
Neste caso são utilizadas structs para realizar o parse do dado. Ex:
```go
package main
import "fmt"
import "encoding/json"

type App struct {
	Id string `json:"id"`
	Title string `json:"title"`
}

func main() {
    // data simula um json neste exemplo
	data := []byte(`
		{
			"id": "Marshal",
			"title": "first"
		}
	`)

	var app App
	err := json.Unmarshal(data, &app)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println(app.Id)
}

Saída: Marshal
```

### Campos aninhado (nested fields)
Jsons podem possuir objetos dentro de outros objetos, neste caso structs permitem o uso de outras structs para os campos. Ex:
```go
package main
import "fmt"
import "encoding/json"

type Library struct {
	Id string `json:"library_id"`
	Name string `json:"name"`
}

type Book struct {
	Id string `json:"id"`
	Title string `json:"title"`
	Library Library `json:"library"`
}

func main() {
	// data simula um json neste exemplo
	data := []byte(`
		{
			"id": "Marshal",
			"title": "first",
			"library":{
				"library_id":"okok",
				"name":"testr"
			}
		}
	`)

	var book Book
	err := json.Unmarshal(data, &book)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println(book)
}

Saída: {Marshal first {okok testr}}
```

### Campo vazio e omitempty
Caso o json não possua o campo especificado na struct, o campo estará com o valor padrão (ou seja, seu equivalente a vazio (0 para int, "" para string etc)). Ex:
```go
package main
import "fmt"
import "encoding/json"

type App struct {
	Id string `json:"id"`
	Number int64 `json:"title"`
}

func main() {
	// data simula um json neste exemplo
	data := []byte(`
		{
			"id": "Marshal"
		}
	`)

	var app App
	err := json.Unmarshal(data, &app)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println(app.Number)
}

Saída: 0
```

Porém é possível utilizar o `omitempty`, uma flag que permite remover `chaves` que possuem os valores vazios respectivos de seus tipos de dados. Ex:
```go
package main
import "fmt"
import "encoding/json"

type Dog struct {
	Breed    string
	WeightKg int `json:",omitempty"`
}

func main() {
	d := Dog{
		Breed:    "pug",
	}
	b, _ := json.Marshal(d)
	fmt.Println(string(b))
}

Saída: {"Breed":"pug"}
```

## Json dinâmico
Aqui a expressão `dinâmico`, significa que o json vai possuir formatos (chaves e valores) que não são previamente definidos. Para este caso serão tratadas duas soluções: `interface` e `fastjson`.

### Interfaces
Em Go, `interfaces` são variáveis que aceitam qualquer tipo de dados, ou seja, o go vai reservar espaço de memória suficiente pra qualquer tipo de dado que quiser armazenar. Ex:
```go
package main
import "fmt"
import "encoding/json"

func main() {
	// data simula um json neste exemplo
	data := []byte(`
		{
			"id": "Marshal",
			"title": "first",
			"library":{
				"library_id":"okok",
				"name":"testr"
			}
		}
	`)

	var book interface{}
	err := json.Unmarshal(data, &book)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println(book)
}

Saída: map[id:Marshal library:map[library_id:okok name:testr] title:first]
```

#### Objetos ou arrays
Caso saiba qual o tipo de dado que virá (se será objeto ou array), é possível utilizar duas versões do `interface` que realizam o parse de arrays e objets aritrários. Ex:
```go
package main
import "fmt"
import "encoding/json"

type Person struct {
	Name string `json:"Name"`
	Age int `json:"Age"`
	Parents []interface{} `json:Parents`
	Address map[string]interface{} `json:address`
}

func main() {
	// data simula um json neste exemplo
	data := []byte(`
		{
			"Name": "Eve",
			"Age": 6,
			"Parents": [
				"Alice",
				"Bob"
			],
			"address": {
				"street": "1",
				"city": "NY"
			}
		}
	`)

	var person Person
	err := json.Unmarshal(data, &person)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println(person)
	fmt.Println(person.Address["city"])
	fmt.Println(person.Parents[0])
}

Saída: {Eve 6 [Alice Bob] map[city:NY street:1]}
NY
Alice
```
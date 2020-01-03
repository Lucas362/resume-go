# Fastjson
A introdução deste parser se encontra no arquivo `json.md`. Aqui serão tratados exemplos de seus métodos e usabilidades, como forma de resumo.

## Exists
Retorna `true` caso a chave especificada se encontra no Json, e `false` caso contrário. Declaração:
```go
func Exists(data []byte, keys string) bool
```

Ex:
```go
package main
import "fmt"
import "github.com/valyala/fastjson"

func main() {
	// data simula um json neste exemplo
	data := (`
	{
		"data":[{
		   "a":{
			  "b":{
				 "c":[]
			  }
		   }
		}
		]
	 }
	`)

	var p fastjson.Parser
	v, _ := p.Parse(data)

	fmt.Println(v.Exists("data"))
	fmt.Println(v.Exists("month"))
}

Saída: true
false
```

## Validate
Valida o Json. Retorna `nil` caso o json esteja correto, e erro caso o json não esteja correto. Exemplo correto:
```go
package main
import "fmt"
import "github.com/valyala/fastjson"

func main() {
	// data simula um json neste exemplo
	data := (`
	{
		"data":[{
		   "a":{
			  "b":{
				 "c":[]
			  }
		   }
		}
		]
	 }
	`)

	fmt.Println(fastjson.Validate(data))
}

Saída: <nil>
```

Ex caso formato errado:
```go
package main
import "fmt"
import "github.com/valyala/fastjson"

func main() {
	// data simula um json neste exemplo
	data := (`
	{
		"data":{
		   "a":{
			  "b":{
				 "c":[]
			  }
		   }
		}
		]
	 }
	`)

	fmt.Println(fastjson.Validate(data))
}

Saída: cannot parse JSON: cannot parse object: missing ',' after object value; unparsed tail: "]\n\t }\n\t"
```

## ValidateBytes
Funciona como o `validate`, mas recebe `[]byte` ao invés de `string`. Declaração:
```go
func ValidateBytes(b []byte) error
```

## 
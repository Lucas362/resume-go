# Json
Por ser uma linguagem fortemente tipada (todas as variáveis tem um tipo específico desde de sua criação até o fim da execução), realizar um parse de json é relativamente problemático. Aqui serão mostradas duas formas de tratar json, a forma estática e a forma dinâmica.

## Json estático
Com json estático, estamos nos referindo a json onde todas as chaves e seus tipos de valor correspondentes são conhecidos e não vão mudar. 

### Structures
Neste caso são utilizadas structures para realizar o parse do dado. Ex:
```go
package main
import "fmt"
import "encoding/json"

type App struct {
	Id string `json:"id"`
	Title string `json:"title"`
}

func main() {
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
```

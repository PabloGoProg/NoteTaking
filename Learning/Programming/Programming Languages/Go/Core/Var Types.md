### Tipos de Variables Permitidos por Go

```
bool -> true / false | flag :: default = false
string -> "Representación de Texto" :: default = ""
int --> Número entero (No determina el tamaño máximo del int)
- uint -> Entero sin signo (No negativo) :: default = 0
float32, 64 -> Números de Coma Flotante :: default = 0
byte -> (uint8) - Usado para representar binarios :: default = 0
rune -> (int32) - Caracteres UNIT8 :: default = 0
complex64, 128 -> Parte real + parte imaginaria -> N + iN :: default = 0 + 0N
```

## Instancia de Variables

```Go
var numero int = 10 // Definición + Asignación

var numero2 int  // Definción
numero2 = 10     // Asignación

numero3 := 10    // Inferencia de Tipo + Definición + Asigancion

// ---------

dec = := 3.1416
sum = numero3 + int(dec) // Casteo de Tipos
```

- Crear una variable por fuera del método principal de un `file`, permite que pueda ser referenciada en cualquier `scope`.

### Arrays

``` Go
fixedArray := [3]int{1, 2, 3} // Requieren de un tamaño para ser utilizados
variableArray := []int{4, 5, 6} // No requieren de un longitud fija

array[2] = 4 // --> Reasignación en dijos y variables
array = append(array, 4) // Insert in dynamic arrays
```
### Maps

```Go
dict := map[string]int{
	"Edad": 18,
}

dict"Altura" = 178
```
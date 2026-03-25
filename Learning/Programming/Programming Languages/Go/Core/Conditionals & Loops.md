### Condicionales

```Go
if edad >= 18 {
	fmt.Println("Persona Mayor de Edad")
} else {
	fmt.Println("Persona Menor de Edad")
}

// No existe un ternario por defecto en Go, se puede recrear con funciones
func If[T any](condition bool, trueVal, falseVal T) T {
    if condition {
        return trueVal
    }
    return falseVal
}

status = If(true, "Active", "Inactive")

// Switch Cases
value := 2
switch value {
	case 1:
		fmt.Printf("%d", value)
	case 2:
		fmt.Printf("%d", value)
	...
	default
		fmt.Printf("Not found")
}
```

### Loops

```Go
// For Loop Normal
for i:= 0; i < 5; i++ {
	fmt.Printf("%d", i)
}

// While Loop
for n < 3 { 
	fmt.Printf("%d", i)
}

// Loop infinito
var i int
for {
	fmt.Printf("%d", i)
	i++
}

// Range For -> Iteración de Slices
for index, value := range slice {
	fmt.Printf("Indice: %d, Valor: %d", index, value)
}
```
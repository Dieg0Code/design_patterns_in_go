# Prototype Pattern 🧬

## ¿Qué es el Prototype Pattern? 📝

El patrón de diseño **Prototype** permite crear objetos a partir de otros existentes, funcionando como una "plantilla" o "molde". Similar a cómo en el mundo real los nuevos productos evolucionan de versiones anteriores (iPhone 13, iPhone 14, iPhone 15), este patrón nos permite partir de un diseño base y generar variantes sin comenzar desde cero. 🔄

En lugar de crear objetos complejos desde cero cada vez, clonamos un prototipo existente y lo personalizamos según necesitemos. La clave está en realizar una **copia adecuada** del objeto original.

## El Desafío: Copias Superficiales vs Copias Profundas 🔍

En Go, cuando trabajamos con estructuras que contienen punteros, es esencial entender la diferencia entre:

- **Copia superficial (shallow copy)**: Solo duplica los valores directos y referencias, no los datos apuntados
- **Copia profunda (deep copy)**: Duplica tanto los valores directos como los objetos referenciados

### Ejemplo Ilustrativo 💡

```go
package main

import "fmt"

type Address struct {
    StreetAddress, City, Country string
}

type Person struct {
    Name string
    Address *Address  // Puntero a otra estructura
}

func main() {
    // Creamos nuestro objeto original (prototipo)
    john := Person{
        Name: "John",
        Address: &Address{
            StreetAddress: "123 Main St",
            City: "New York",
            Country: "USA",
        },
    }

    // PROBLEMA: Copia superficial
    jane := john  // Copia los valores, pero Address sigue apuntando al mismo lugar
    jane.Name = "Jane"  // Este cambio es seguro, afecta solo a jane
    jane.Address.StreetAddress = "456 Elm St"  // ¡PELIGRO! Modifica también el original

    fmt.Println("Después de copia superficial:")
    fmt.Printf("John vive en: %s\n", john.Address.StreetAddress)  // "456 Elm St" (¡modificado!)
    fmt.Printf("Jane vive en: %s\n", jane.Address.StreetAddress)  // "456 Elm St"

    // SOLUCIÓN: Copia profunda
    // Reiniciamos john a su estado original
    john.Address.StreetAddress = "123 Main St"

    // Creamos una verdadera copia independiente
    janet := Person{
        Name: john.Name,  // Copiamos el valor simple
        Address: &Address{  // Creamos un NUEVO objeto Address
            StreetAddress: john.Address.StreetAddress,
            City: john.Address.City,
            Country: john.Address.Country,
        },
    }

    janet.Name = "Janet"  // Modificación segura
    janet.Address.StreetAddress = "789 Oak St"  // Ahora es seguro modificar

    fmt.Println("\nDespués de copia profunda:")
    fmt.Printf("John vive en: %s\n", john.Address.StreetAddress)  // "123 Main St" (sin cambios)
    fmt.Printf("Janet vive en: %s\n", janet.Address.StreetAddress)  // "789 Oak St"
}
```

## Deep Copy: La Clave del Prototype Pattern 🔑

La **copia profunda** es esencial para el patrón Prototype porque:

1. Garantiza que el objeto clonado sea totalmente independiente del original
2. Evita efectos secundarios inesperados al modificar cualquiera de los objetos
3. Permite personalizar cada instancia sin afectar a las demás

En estructuras complejas con múltiples niveles de referencia (punteros a objetos que contienen otros punteros), la copia profunda debe realizarse recursivamente en todos los niveles. En Go, esto generalmente implica implementar un método específico de clonación que se encargue de crear copias adecuadas de todas las estructuras anidadas. 🧠

## Implementación Efectiva del Patrón Prototype 🛠️

Para aplicar correctamente este patrón en Go, típicamente implementamos un método `Clone()` o `DeepCopy()` que realiza una copia completa del objeto, incluyendo todas sus estructuras anidadas. En estructuras más complejas, este enfoque permite encapsular la lógica de clonación y garantizar que siempre se realice correctamente.

Este patrón es especialmente valioso cuando la creación de objetos es costosa (requiere acceso a bases de datos, cálculos complejos, etc.) o cuando necesitamos múltiples variantes de un mismo objeto base. 🚀

## Copy Method: Implementando Clonación Profunda 🔄

La implementación efectiva del patrón Prototype en Go requiere crear métodos específicos para realizar copias profundas de estructuras complejas. Estos métodos, comúnmente llamados `DeepCopy()` o `Clone()`, encapsulan la lógica necesaria para duplicar correctamente todos los campos de un objeto, incluyendo sus estructuras anidadas y colecciones. 🧪

### Implementación Paso a Paso 📝

```go
package prototype

import "fmt"

// Estructura que será clonada como parte de otra
type Address struct {
  StreetAddress, City, Country string
}

// Método para crear una copia profunda de Address
func (a *Address) DeepCopy() *Address {
  // Creamos una nueva instancia con los mismos valores
  return &Address{
    StreetAddress: a.StreetAddress,
    City:          a.City,
    Country:       a.Country,
  }
}

// Estructura principal con campos complejos
type Person struct {
  Name    string
  Address *Address    // Puntero a otra estructura
  Friends []string    // Slice (referencia)
}

// Método para crear una copia profunda de Person
func (p *Person) DeepCopy() *Person {
  // Paso 1: Copiamos los valores simples mediante copia de estructura
  q := *p  // Esto copia el campo Name, pero los punteros y referencias siguen apuntando a los mismos datos

  // Paso 2: Copiamos profundamente el objeto Address
  q.Address = p.Address.DeepCopy()

  // Paso 3: Creamos un nuevo slice para Friends y copiamos su contenido
  q.Friends = make([]string, len(p.Friends))
  copy(q.Friends, p.Friends)

  return &q
}

func main() {
  // Creamos la persona original (nuestro prototipo)
  john := Person{
    Name:    "John",
    Address: &Address{
      StreetAddress: "123 London Rd",
      City:          "London",
      Country:       "UK",
    },
    Friends: []string{"Chris", "Matt"},
  }

  // Clonamos el prototipo
  jane := john.DeepCopy()

  // Modificamos la copia
  jane.Name = "Jane"
  jane.Address.StreetAddress = "321 Baker St"
  jane.Friends = append(jane.Friends, "Angela")  // Añadimos un nuevo amigo

  // Verificamos que las modificaciones no afecten al original
  fmt.Println("Original:")
  fmt.Printf("  John: %s\n", john.Name)
  fmt.Printf("  Dirección: %s, %s\n", john.Address.StreetAddress, john.Address.City)
  fmt.Printf("  Amigos: %v\n\n", john.Friends)

  fmt.Println("Copia (modificada):")
  fmt.Printf("  Jane: %s\n", jane.Name)
  fmt.Printf("  Dirección: %s, %s\n", jane.Address.StreetAddress, jane.Address.City)
  fmt.Printf("  Amigos: %v\n", jane.Friends)
}

/* Salida:
Original:
  John: John
  Dirección: 123 London Rd, London
  Amigos: [Chris Matt]

Copia (modificada):
  Jane: Jane
  Dirección: 321 Baker St, London
  Amigos: [Chris Matt Angela]
*/
```

### Puntos Clave para una Implementación Correcta ⚠️

1. **Copia de campos simples**: Los tipos básicos (int, string, bool) se copian automáticamente al copiar la estructura.

2. **Estructuras anidadas**: Cada estructura que contenga punteros debe implementar su propio método `DeepCopy()`.

3. **Colecciones (slices, maps)**:

   - Para slices: Crear un nuevo slice con `make()` y usar `copy()` para duplicar el contenido
   - Para maps: Crear un nuevo map e iterar el original para copiar cada elemento

4. **Recursividad**: Si tus estructuras contienen punteros a otras estructuras complejas, la clonación debe aplicarse recursivamente.

### Casos Especiales y Mejores Prácticas 🔍

- **Campos no exportados**: Si la estructura contiene campos no exportados (minúsculas), considera usar paquetes de serialización como `encoding/json` para realizar la copia profunda.
- **Interfaces**: Para campos que son interfaces, necesitarás implementar lógica específica basada en el tipo concreto subyacente.
- **Ciclos de referencia**: Ten cuidado con estructuras que se referencian circularmente, pues pueden causar recursión infinita. Considera usar un mapa para rastrear objetos ya copiados.

- **Test unitarios**: Siempre verifica que tus métodos `DeepCopy()` funcionen correctamente asegurando que modificar la copia no afecta al original.

El método `DeepCopy()` es la piedra angular del patrón Prototype, ya que encapsula toda la complejidad de crear copias independientes y permite personalizar cada instancia según sea necesario. 🚀

## Copy mediante Serialización: Una Alternativa Elegante 📦

Cuando trabajamos con estructuras complejas o profundamente anidadas, implementar métodos de copia manualmente puede volverse tedioso y propenso a errores. La serialización ofrece una alternativa poderosa: convertimos el objeto completo a un formato binario y luego lo reconstruimos, creando naturalmente una copia profunda sin necesidad de código personalizado para cada campo. 🔄

### Ventajas de la Serialización para Deep Copy 💡

- **Simplicidad**: No es necesario escribir código de copia para cada campo y estructura anidada
- **Completitud**: Garantiza que todos los campos sean copiados, incluso en estructuras complejas
- **Mantenibilidad**: Elimina la necesidad de actualizar el código de copia cuando cambia la estructura

### Implementación con el paquete `encoding/gob` 🛠️

```go
package prototype

import (
  "bytes"
  "encoding/gob"
  "fmt"
  "log"
)

// Estructuras que queremos clonar
type Address struct {
  StreetAddress, City, Country string
}

type Person struct {
  Name    string
  Address *Address
  Friends []string
}

// DeepCopy implementado mediante serialización
func (p *Person) DeepCopy() *Person {
  // Creamos un buffer para almacenar la representación serializada
  b := bytes.Buffer{}

  // Creamos un encoder y serializamos el objeto completo
  e := gob.NewEncoder(&b)
  err := e.Encode(p)
  if err != nil {
    log.Fatalf("Error durante la serialización: %v", err)
  }

  // Opcional: imprimir la representación binaria (bytes)
  // fmt.Printf("Datos serializados: %v bytes\n", b.Len())

  // Creamos un decoder para reconstruir el objeto
  d := gob.NewDecoder(&b)
  result := Person{}

  // Decodificamos los datos en un nuevo objeto
  err = d.Decode(&result)
  if err != nil {
    log.Fatalf("Error durante la deserialización: %v", err)
  }

  return &result
}

func main() {
  // Registramos los tipos para gob (necesario para tipos complejos)
  gob.Register(&Address{})

  // Creamos el objeto original (prototipo)
  john := Person{
    Name: "John",
    Address: &Address{
      StreetAddress: "123 London Rd",
      City: "London",
      Country: "UK",
    },
    Friends: []string{"Chris", "Matt", "Sam"},
  }

  // Creamos una copia utilizando serialización
  jane := john.DeepCopy()

  // Modificamos la copia
  jane.Name = "Jane"
  jane.Address.StreetAddress = "321 Baker St"
  jane.Friends = append(jane.Friends, "Jill")

  // Verificamos que ambos objetos son independientes
  fmt.Println("Original:")
  fmt.Printf("  Nombre: %s\n", john.Name)
  fmt.Printf("  Dirección: %s, %s\n", john.Address.StreetAddress, john.Address.City)
  fmt.Printf("  Amigos: %v\n\n", john.Friends)

  fmt.Println("Copia (modificada):")
  fmt.Printf("  Nombre: %s\n", jane.Name)
  fmt.Printf("  Dirección: %s, %s\n", jane.Address.StreetAddress, jane.Address.City)
  fmt.Printf("  Amigos: %v\n", jane.Friends)

  /* Salida:
  Original:
    Nombre: John
    Dirección: 123 London Rd, London
    Amigos: [Chris Matt Sam]

  Copia (modificada):
    Nombre: Jane
    Dirección: 321 Baker St, London
    Amigos: [Chris Matt Sam Jill]
  */
}
```

### Consideraciones Importantes ⚠️

1. **Rendimiento**: La serialización puede ser menos eficiente que la copia manual para estructuras simples.

2. **Compatibilidad**: Las estructuras deben ser serializables - todos los campos deben ser exportados (comenzar con mayúscula) o se perderán durante la copia.

3. **Tipos Personalizados**: Para tipos complejos o personalizados, puede ser necesario registrarlos con `gob.Register()`.

4. **Alternativas**: Además de `gob`, puedes usar otros formatos de serialización:
   - `encoding/json`: Más flexible pero menos eficiente
   - `encoding/xml`: Útil si necesitas interoperabilidad externa
   - Bibliotecas de terceros como MessagePack o Protocol Buffers para mayor rendimiento

### ¿Cuándo usar este enfoque? 🤔

La serialización para deep copy es ideal cuando:

- Tienes estructuras complejas con muchos niveles de anidamiento
- La estructura cambia con frecuencia (evitas mantener código de copia)
- La legibilidad y mantenibilidad son más importantes que el rendimiento óptimo

Este método proporciona una solución elegante y genérica al desafío del deep copying en Go, simplificando significativamente la implementación del patrón Prototype. 🚀

## Prototype Factory: Combinando Prototipos y Factories 🏭

El **Prototype Factory** es una poderosa combinación de los patrones Prototype y Factory que utiliza objetos prototípicos predefinidos como base para crear nuevas instancias personalizadas. Este enfoque resulta especialmente valioso cuando:

- Muchos objetos comparten una configuración base común pero varían en algunos detalles
- Quieres centralizar la lógica de creación mientras mantienes la flexibilidad de personalización
- Necesitas ocultar la complejidad de la inicialización de objetos

### Implementación con Prototipos Predefinidos 🧪

```go
package main

import (
  "bytes"
  "encoding/gob"
  "fmt"
  "log"
)

// Estructura de dirección con detalles específicos
type Address struct {
  Suite int             // Número de oficina
  StreetAddress, City string
}

// Empleado con información básica y ubicación
type Employee struct {
  Name string
  Office Address
}

// Método para crear copia profunda mediante serialización
func (p *Employee) DeepCopy() *Employee {
  b := bytes.Buffer{}
  e := gob.NewEncoder(&b)
  err := e.Encode(p)
  if err != nil {
    log.Fatalf("Error al serializar: %v", err)
    return nil
  }

  d := gob.NewDecoder(&b)
  result := Employee{}
  err = d.Decode(&result)
  if err != nil {
    log.Fatalf("Error al deserializar: %v", err)
    return nil
  }
  return &result
}

// ---- PROTOTYPE FACTORY ----

// Objetos prototípicos predefinidos (plantillas base)
var mainOffice = Employee{
  "", // Nombre vacío (se establecerá después)
  Address{0, "123 East Dr", "London"}, // Dirección de la oficina principal
}

var auxOffice = Employee{
  "", // Nombre vacío (se establecerá después)
  Address{0, "66 West Dr", "London"}, // Dirección de la oficina auxiliar
}

// Función interna para configurar un empleado basado en un prototipo
// Nota: minúsculas = función privada, solo para uso interno
func newEmployee(proto *Employee, name string, suite int) *Employee {
  result := proto.DeepCopy()   // Creamos una copia profunda del prototipo
  result.Name = name           // Personalizamos el nombre
  result.Office.Suite = suite  // Asignamos número de oficina
  return result
}

// Funciones Factory públicas - abstraen la selección de prototipo

// Crea un empleado en la oficina principal
func NewMainOfficeEmployee(name string, suite int) *Employee {
  return newEmployee(&mainOffice, name, suite)
}

// Crea un empleado en la oficina auxiliar
func NewAuxOfficeEmployee(name string, suite int) *Employee {
  return newEmployee(&auxOffice, name, suite)
}

func main() {
  // Creamos empleados utilizando las factories especializadas
  john := NewMainOfficeEmployee("John", 100)
  jane := NewAuxOfficeEmployee("Jane", 200)

  // Verificamos que los empleados tienen las configuraciones correctas
  fmt.Printf("John trabaja en: %s, Suite %d\n",
             john.Office.StreetAddress, john.Office.Suite)
  fmt.Printf("Jane trabaja en: %s, Suite %d\n",
             jane.Office.StreetAddress, jane.Office.Suite)

  /* Salida:
  John trabaja en: 123 East Dr, Suite 100
  Jane trabaja en: 66 West Dr, Suite 200
  */
}
```

### Ventajas del Prototype Factory 💪

1. **Configuración centralizada** 🎯 - Las plantillas prototípicas definen valores predeterminados en un solo lugar, facilitando cambios globales

2. **APIs simplificadas** 📋 - Los clientes solo necesitan proporcionar información específica (nombre y número de oficina), no todos los detalles

3. **Flexibilidad con coherencia** 🔄 - Cada objeto creado hereda la configuración base pero puede personalizarse según sea necesario

4. **Escalabilidad** 🚀 - Añadir nuevos tipos de empleados (como `RemoteEmployee`) solo requiere definir un nuevo prototipo y una función factory

### Observaciones Clave 🔍

En este patrón:

- Los **prototipos** son los objetos base con valores predeterminados (`mainOffice`, `auxOffice`)
- Las **factories** proporcionan una interfaz limpia para crear instancias (`NewMainOfficeEmployee`, `NewAuxOfficeEmployee`)
- La **clonación** mediante `DeepCopy()` garantiza que las modificaciones no afecten a los prototipos originales

Este enfoque es particularmente eficaz en sistemas que tienen configuraciones con variantes predefinidas, como diferentes tipos de usuarios, documentos, o configuraciones regionales. 🌍

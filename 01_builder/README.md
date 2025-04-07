# Builder Pattern 🏗️

## ¿Qué es el Builder Pattern? 🤔

El **Builder Pattern** es un patrón de diseño creacional que permite construir objetos complejos paso a paso. Este patrón es esencial cuando:

- Un objeto tiene numerosas propiedades, muchas opcionales ⚙️
- El proceso de construcción requiere múltiples pasos en un orden específico 📋
- Diferentes representaciones del mismo objeto deben ser creadas usando el mismo proceso 🔄

En esencia: _Cuando la construcción de un objeto es compleja, el Builder proporciona una API clara y fluida para construirlo paso a paso._

## El Problema 🚫

Construir objetos complejos directamente puede llevar a:

```go
// Código difícil de leer con múltiples parámetros
document := NewDocument("Report", "Annual", 12, true, "PDF",
                        "A4", true, "Company", "Header", "Footer",
                        "Portrait", 300, "normal")

// O constructores múltiples difíciles de mantener
doc1 := NewSimpleDocument("Report")
doc2 := NewDocumentWithFormat("Report", "PDF", "A4")
doc3 := NewCompleteDocument("Report", "PDF", "A4", "Header", "Footer")
```

## La Solución: Builder Pattern 💡

### Un Ejemplo Práctico: Generación de HTML

Veamos primero un enfoque sin patrón usando `strings.Builder` integrado en Go:

```go
package main

import (
  "fmt"
  "strings"
)

func main() {
  // Ejemplo 1: Generación HTML simple
  hello := "hello"
  sb := strings.Builder{}
  sb.WriteString("<p>")
  sb.WriteString(hello)
  sb.WriteString("</p>")
  fmt.Printf("%s\n", sb.String())  // <p>hello</p>

  // Ejemplo 2: HTML más complejo - difícil de mantener
  words := []string{"hello", "world"}
  sb.Reset()
  sb.WriteString("<ul>")
  for _, v := range words {
    sb.WriteString("<li>")
    sb.WriteString(v)
    sb.WriteString("</li>")
  }
  sb.WriteString("</ul>")
  fmt.Println(sb.String())  // <ul><li>hello</li><li>world</li></ul>
}
```

### Implementando Builder Pattern para HTML 🧱

Ahora, aplicamos el patrón Builder para hacer la construcción más clara y mantenible:

```go
package main

import (
  "fmt"
  "strings"
)

const (
  indentSize = 2  // Espacios para la indentación
)

// 1️⃣ El producto complejo que queremos construir
type HtmlElement struct {
  name, text string
  elements []HtmlElement
}

// Método para convertir el elemento HTML a string
func (e *HtmlElement) String() string {
  return e.string(0)
}

// Método privado para manejar la indentación
func (e *HtmlElement) string(indent int) string {
  sb := strings.Builder{}
  i := strings.Repeat(" ", indentSize * indent)

  // Abre la etiqueta
  sb.WriteString(fmt.Sprintf("%s<%s>\n", i, e.name))

  // Añade el texto si existe
  if len(e.text) > 0 {
    sb.WriteString(strings.Repeat(" ", indentSize * (indent + 1)))
    sb.WriteString(e.text)
    sb.WriteString("\n")
  }

  // Añade los elementos hijos recursivamente
  for _, el := range e.elements {
    sb.WriteString(el.string(indent+1))
  }

  // Cierra la etiqueta
  sb.WriteString(fmt.Sprintf("%s</%s>\n", i, e.name))
  return sb.String()
}

// 2️⃣ El Builder para HtmlElement
type HtmlBuilder struct {
  rootName string
  root HtmlElement
}

// Constructor del Builder
func NewHtmlBuilder(rootName string) *HtmlBuilder {
  return &HtmlBuilder{
    rootName: rootName,
    root: HtmlElement{
      name: rootName,
      text: "",
      elements: []HtmlElement{},
    },
  }
}

// Método para obtener el resultado final
func (b *HtmlBuilder) String() string {
  return b.root.String()
}

// Método para añadir un hijo (versión simple)
func (b *HtmlBuilder) AddChild(childName, childText string) {
  e := HtmlElement{childName, childText, []HtmlElement{}}
  b.root.elements = append(b.root.elements, e)
}

// 3️⃣ Método fluido (versión mejorada que permite encadenamiento)
func (b *HtmlBuilder) AddChildFluent(childName, childText string) *HtmlBuilder {
  e := HtmlElement{childName, childText, []HtmlElement{}}
  b.root.elements = append(b.root.elements, e)
  return b  // Retorna el builder para permitir encadenamiento
}

func main() {
  // La API fluida del builder en acción
  builder := NewHtmlBuilder("ul")
  builder.AddChildFluent("li", "hello").
    AddChildFluent("li", "world")

  fmt.Println(builder.String())

  /* Salida:
  <ul>
    <li>
      hello
    </li>
    <li>
      world
    </li>
  </ul>
  */
}
```

## Ventajas del Builder 💪

- **Construcción paso a paso**: Permite crear objetos complejos incrementalmente 🧪
- **Código más legible**: La API fluida crea código declarativo y autoexplicativo 📝
- **Evita constructores telescópicos**: Elimina la necesidad de múltiples constructores con diferentes parámetros 🔍
- **Mayor control**: Permite validaciones durante la construcción del objeto 🛡️
- **Inmutabilidad**: Puede facilitar la creación de objetos inmutables 🔒

## Aplicaciones Reales en Go 🌐

El Builder Pattern se usa frecuentemente en:

- Construcción de consultas SQL
- Configuración de servidores HTTP
- Creación de objetos de petición/respuesta
- Generación de documentos (PDF, HTML)
- Configuración de opciones para bibliotecas

## Builder vs. Factory 🤝

Mientras que un Factory simplemente crea e instancia objetos directamente, el Builder se enfoca en la construcción paso a paso cuando el proceso es complejo o cuando se requieren múltiples pasos configurables.

Builder brilla especialmente cuando necesitas una API clara y expresiva para construir objetos con numerosas opciones configurables. 🌟

## Builder Facets: Construyendo Objetos Complejos por Capas 🧩

En la mayoría de implementaciones, un solo Builder es suficiente. Sin embargo, cuando construimos objetos con **grupos lógicos de propiedades**, puede ser más elegante separar la construcción por aspectos o "facetas". Este enfoque permite crear una API más expresiva y organizada por dominios conceptuales. 🔍

### El Desafío: Objetos con Múltiples Aspectos 🤔

Considere un objeto `Person` que contiene información tanto personal como profesional:

```go
package main

type Person struct {
    // Información de dirección
    StreetAddress, Postcode, City string

    // Información laboral
    CompanyName, Position string
    AnnualIncome int
}
```

Un builder tradicional mezclaría métodos para configurar dirección y empleo en una sola interfaz, resultando en una API menos intuitiva. ¿Cómo podemos organizar esto mejor?

### Solución: Builders Especializados con Facetas 🛠️

El patrón Builder con facetas utiliza múltiples builders coordinados que:

1. Comparten acceso al mismo objeto en construcción
2. Proporcionan interfaces específicas para cada aspecto
3. Permiten transiciones fluidas entre diferentes aspectos

```go
package main

import "fmt"

// 1️⃣ Estructura que queremos construir
type Person struct {
  // Faceta de dirección
  StreetAddress, Postcode, City string

  // Faceta de información laboral
  CompanyName, Position string
  AnnualIncome int
}

// 2️⃣ Builder principal que coordina los sub-builders
type PersonBuilder struct {
  person *Person  // Todos los builders operan sobre la misma instancia
}

func NewPersonBuilder() *PersonBuilder {
  return &PersonBuilder{&Person{}}
}

// Método para obtener el objeto construido
func (b *PersonBuilder) Build() *Person {
  return b.person
}

// 3️⃣ Métodos para acceder a builders especializados
// Retorna el builder para información laboral
func (b *PersonBuilder) Works() *PersonJobBuilder {
  return &PersonJobBuilder{*b}
}

// Retorna el builder para información de dirección
func (b *PersonBuilder) Lives() *PersonAddressBuilder {
  return &PersonAddressBuilder{*b}
}

// 4️⃣ Builder especializado para información laboral
type PersonJobBuilder struct {
  PersonBuilder
}

func (b *PersonJobBuilder) At(companyName string) *PersonJobBuilder {
  b.person.CompanyName = companyName
  return b
}

func (b *PersonJobBuilder) AsA(position string) *PersonJobBuilder {
  b.person.Position = position
  return b
}

func (b *PersonJobBuilder) Earning(annualIncome int) *PersonJobBuilder {
  b.person.AnnualIncome = annualIncome
  return b
}

// 5️⃣ Builder especializado para información de dirección
type PersonAddressBuilder struct {
  PersonBuilder
}

func (b *PersonAddressBuilder) At(streetAddress string) *PersonAddressBuilder {
  b.person.StreetAddress = streetAddress
  return b
}

func (b *PersonAddressBuilder) In(city string) *PersonAddressBuilder {
  b.person.City = city
  return b
}

func (b *PersonAddressBuilder) WithPostcode(postcode string) *PersonAddressBuilder {
  b.person.Postcode = postcode
  return b
}

func main() {
  // 6️⃣ Construcción del objeto usando la API fluida con múltiples builders
  pb := NewPersonBuilder()
  person := pb.
    Lives().                         // Cambia al builder de dirección
      At("123 London Road").
      In("London").
      WithPostcode("SW12BC").
    Works().                         // Cambia al builder de trabajo
      At("Fabrikam").
      AsA("Programmer").
      Earning(123000).
    Build()                          // Finaliza la construcción

  fmt.Println(*person)
  // Salida: {123 London Road SW12BC London Fabrikam Programmer 123000}
}
```

### ¿Cómo Funciona? 🔄

1. El **PersonBuilder** principal mantiene una referencia al objeto `Person` en construcción
2. Cada builder especializado (**PersonJobBuilder** y **PersonAddressBuilder**) embebe el builder principal
3. Los métodos `Lives()` y `Works()` facilitan la transición entre builders especializados
4. Todos los builders operan sobre la misma instancia de `Person`
5. Cada builder devuelve una referencia a sí mismo para permitir el encadenamiento fluido

### Ventajas del Builder con Facetas 🌟

- **Código más expresivo**: La API comunica claramente los diferentes aspectos del objeto ✨
- **Mejor organización**: Separa la lógica de construcción por dominios conceptuales 📊
- **Mayor mantenibilidad**: Facilita añadir nuevas propiedades a cada aspecto sin afectar otros 🔧
- **Validación específica**: Cada builder puede implementar validaciones propias de su dominio 🛡️

Este patrón es particularmente útil para objetos complejos que representan diferentes conceptos de negocio o que tienen conjuntos lógicos de propiedades claramente separados. 🎯

## Builder Parameter: Forzando el Uso del Builder 🔒

Una pregunta común es: **¿Cómo puedo asegurar que se use mi Builder en lugar de crear objetos directamente?** Una estrategia efectiva consiste en hacer privadas las estructuras que deseamos proteger y exponer únicamente APIs basadas en Builder para su construcción. 🛡️

### El Problema: Construcción Descontrolada ⚠️

Consideremos este ejemplo simple de envío de emails:

```go
package main

type email struct {
  to, from, subject, body string
}

func SendEmail(email email)

func main() {}
```

Con esta implementación, enfrentamos varios problemas:

- Los usuarios pueden crear emails incompletos o malformados
- No hay validación durante la construcción
- Resulta difícil añadir validaciones posteriores sin modificar código existente

### La Solución: Builder Forzado con Funciones de Configuración 🔐

Podemos resolver estos problemas ocultando la estructura `email` (usando minúsculas para hacerla no exportable) y proporcionando una API basada en builders que obligue a seguir el proceso correcto:

```go
package main

import "strings"

// Estructura no exportable (privada)
type email struct {
    from, to, subject, body string
}

// Builder público para configurar emails
type EmailBuilder struct {
    email email
}

// Método con validación incorporada
func (b *EmailBuilder) From(from string) *EmailBuilder {
    if !strings.Contains(from, "@") {
        panic("email should contain @")
    }
    b.email.from = from
    return b
}

func (b *EmailBuilder) To(to string) *EmailBuilder {
    b.email.to = to
    return b
}

func (b *EmailBuilder) Subject(subject string) *EmailBuilder {
    b.email.subject = subject
    return b
}

func (b *EmailBuilder) Body(body string) *EmailBuilder {
    b.email.body = body
    return b
}

// Implementación real del envío (privada)
func sendMailImpl(email *email) {
    // Código que realmente envía el email
}

// 🔑 El patrón clave: función que acepta un configurador
type build func(*EmailBuilder)

// API pública que fuerza el uso del builder
func SendEmail(action build) {
    builder := EmailBuilder{}
    action(&builder)
    sendMailImpl(&builder.email)
}

func main() {
    // Uso elegante con función anónima como configurador
    SendEmail(func(b *EmailBuilder) {
        b.From("foo@bar.com").
            To("bar@baz.com").
            Subject("Meeting").
            Body("Hello, do you want to meet?")
    })
}
```

### ¿Cómo Funciona? 🧠

Esta implementación utiliza un enfoque ingenioso:

1. **Estructura privada**: `email` es no exportable, impidiendo su creación directa desde paquetes externos
2. **Tipo de función configuradora**: `type build func(*EmailBuilder)` define un tipo para funciones que configuran un builder
3. **API pública con inyección**: `SendEmail()` acepta una función configuradora, crea el builder y lo pasa a la función
4. **Validación integrada**: Los métodos del builder pueden validar cada campo (como el formato de email)
5. **Construcción controlada**: Solo `sendMailImpl()` accede al objeto email final, garantizando su completitud

### Beneficios de Este Enfoque 💪

- **Control total del proceso de creación** ✅ - Garantiza que todos los objetos se construyan correctamente
- **Validaciones integradas** 🛡️ - Cada setter puede incluir validaciones específicas
- **API expresiva y fluida** 📝 - Los usuarios disfrutan de una interfaz limpia y encadenable
- **Desacoplamiento** 🔄 - El código cliente no depende de detalles de implementación
- **Testabilidad mejorada** 🧪 - La función configuradora facilita el mock en pruebas

Este patrón es particularmente valioso en bibliotecas y APIs públicas donde necesitas garantizar que los objetos siempre se creen correctamente, siguiendo todas las reglas de negocio y validaciones necesarias. 🏆

## Functional Builder: Composición de Modificaciones 🧩

El patrón **Functional Builder** representa una evolución elegante del Builder tradicional, adoptando un enfoque funcional para la construcción de objetos. En lugar de métodos que modifican directamente el estado del objeto en construcción, este patrón utiliza una colección de funciones que se aplicarán posteriormente, ofreciendo mayor flexibilidad y componibilidad. 🔄

### El Concepto: Funciones como Bloques de Construcción 🧱

El Functional Builder almacena una serie de funciones modificadoras que se aplicarán a un objeto cuando se finalice la construcción. Este enfoque tiene varias ventajas:

- Permite componer modificaciones de forma dinámica
- Facilita la extensión del builder sin modificar el código existente
- Posibilita la creación de builders especializados mediante composición

### Implementación en Go 💻

```go
package main

import "fmt"

// 1️⃣ El producto que queremos construir
type Person struct {
  name, position string
}

// 2️⃣ Definimos un tipo para nuestras funciones modificadoras
type personMod func(*Person)

// 3️⃣ El Builder funcional almacena acciones en lugar de datos
type PersonBuilder struct {
  actions []personMod  // Lista de modificaciones a aplicar
}

// 4️⃣ Cada método añade una nueva función modificadora a la lista
func (b *PersonBuilder) Called(name string) *PersonBuilder {
  b.actions = append(b.actions, func(p *Person) {
    p.name = name  // Esta función se ejecutará después
  })
  return b
}

// 5️⃣ El método Build aplica todas las modificaciones en secuencia
func (b *PersonBuilder) Build() *Person {
  p := Person{}  // Creamos un objeto vacío
  for _, action := range b.actions {
    action(&p)   // Aplicamos cada modificación
  }
  return &p
}

// 6️⃣ Podemos extender fácilmente con nuevos métodos
func (b *PersonBuilder) WorksAsA(position string) *PersonBuilder {
  b.actions = append(b.actions, func(p *Person) {
    p.position = position
  })
  return b
}

// 7️⃣ Ejemplo de extensión por composición
type EmployeeBuilder struct {
  PersonBuilder  // Reutilizamos toda la funcionalidad
}

// Añadimos métodos específicos para empleados
func (b *EmployeeBuilder) WithSalary(salary int) *EmployeeBuilder {
  b.actions = append(b.actions, func(p *Person) {
    // Imaginemos que existe un campo salary que podríamos establecer
    fmt.Printf("Setting salary to %d for %s\n", salary, p.name)
  })
  return b
}

func main() {
  // Uso básico
  b := PersonBuilder{}
  p := b.Called("Dmitri").WorksAsA("Developer").Build()
  fmt.Println(*p)  // Salida: {Dmitri Developer}

  // Uso con builder extendido
  eb := EmployeeBuilder{}
  employee := eb.Called("Alex").
                WorksAsA("Engineer").
                WithSalary(75000).
                Build()
  fmt.Println(*employee)  // Salida: {Alex Engineer}
}
```

### Ventajas del Functional Builder 🌟

- **Componibilidad**: Las funciones modificadoras pueden combinarse libremente 🧬
- **Extensibilidad**: Nuevas funcionalidades pueden añadirse sin alterar código existente 🔌
- **Reutilización**: Las mismas modificaciones pueden aplicarse a diferentes objetos 🔁
- **Separación de preocupaciones**: Cada función modificadora tiene una única responsabilidad 🎯
- **Evaluación diferida**: Las modificaciones se almacenan y ejecutan solo cuando se llama a Build() ⏱️

### Aplicaciones Ideales 💼

El Functional Builder brilla particularmente en escenarios donde:

- Necesitas componentes de construcción que puedan reutilizarse en diferentes contextos
- Los objetos tienen múltiples configuraciones opcionales o relacionadas
- Quieres permitir que otros desarrolladores extiendan tus builders sin modificar tu código
- Trabajas con sistemas que requieren transformaciones encadenadas de datos

Este enfoque funcional para el patrón Builder demuestra cómo los principios de la programación funcional pueden enriquecer los patrones de diseño tradicionales, proporcionando soluciones más flexibles y componibles. 🚀

## Sumario: Builder Pattern en Go 🏗️

- Un Builder es un componente separado que construye un objeto complejo paso a paso.
- Para hacer que un builder sea fluido, devuelves el mismo builder en cada método. Permitiendo encadenar llamadas.
- Diferentes aspectos de un objeto pueden ser construidos con diferentes Builders especializados.

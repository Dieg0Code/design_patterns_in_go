# Patrones de Diseño en Golang: Soluciones Probadas para Desafíos Comunes 🧠

## La Esencia de los Patrones de Diseño 🌟

Los **Patrones de Diseño** son soluciones efectivas desarrolladas por programadores a lo largo del tiempo para resolver problemas recurrentes en el desarrollo de software. 🏛️ Son como plantillas probadas que pueden adaptarse a situaciones específicas, ofreciendo estructura y flexibilidad a la vez.

A diferencia de una biblioteca que importas y usas directamente, un patrón ofrece una perspectiva, un enfoque para abordar un problema. ⚡ No es código listo para usar, sino un concepto que debes implementar según tus necesidades, similar a cómo un ajedrecista reconoce situaciones de juego sin memorizar cada movimiento posible.

## Patrones vs. Algoritmos: Diferencias Clave 🔮

Estos dos conceptos fundamentales en programación tienen propósitos distintos:

🔸 **Algoritmos**: Secuencias precisas de pasos que resuelven problemas específicos con resultados predecibles, como un procedimiento bien definido que siempre produce el mismo resultado cuando se siguen los mismos pasos.

🔸 **Patrones**: Marcos conceptuales que organizan relaciones entre componentes, comparable a un plano arquitectónico que permite múltiples implementaciones manteniendo los mismos principios estructurales.

Dos programadores pueden implementar el mismo patrón y crear código muy diferente, aunque ambas soluciones aborden el mismo problema fundamental. 🎻

## Anatomía de un Patrón de Diseño 📘

Los patrones se documentan siguiendo una estructura clara:

- 🎯 **Propósito**: Descripción concisa del problema y su solución
- 💎 **Motivación**: Contexto que explica por qué el patrón es necesario
- 🧩 **Estructura**: Representación formal de componentes y relaciones
- ⚙️ **Implementación**: Ejemplos en código que muestran cómo aplicar el patrón

Los recursos más completos también incluyen información sobre variantes, consecuencias y relaciones con otros patrones. 📚

## Historia de los Patrones de Diseño 🌿

### Origen Práctico 🌱

Los patrones de diseño surgieron naturalmente de la experiencia práctica. No fueron inventados en abstracto, sino descubiertos cuando programadores notaron soluciones similares que aparecían repetidamente en diferentes proyectos. Son el resultado de observar y documentar buenas prácticas que emergían orgánicamente en el desarrollo de software. 🧭

### La Inspiración de la Arquitectura 🏛️

El concepto viene originalmente de Christopher Alexander, un arquitecto que creó la idea de "lenguaje de patrones" para documentar principios recurrentes en arquitectura y urbanismo: desde la altura ideal de ventanas hasta la disposición de espacios públicos en vecindarios.

### La Gang of Four 🧠

La aplicación al software ocurrió en 1995, cuando Erich Gamma, John Vlissides, Ralph Johnson y Richard Helm publicaron "Design Patterns: Elements of Reusable Object-Oriented Software". Este influyente libro documentó 23 patrones fundamentales para la programación orientada a objetos.

Por su título extenso, la comunidad comenzó a llamarlo "el libro de la Gang of Four" o simplemente "GoF", un apodo que persiste hasta hoy. 📖

### Evolución Continua 🚀

Desde entonces, el conocimiento sobre patrones ha crecido enormemente, extendiéndose más allá de la programación orientada a objetos hacia prácticamente todos los ámbitos del desarrollo de software, desde microservicios hasta interfaces de usuario.

## El Valor Práctico de los Patrones 💡

Es posible desarrollar software durante años sin conocer formalmente los patrones, y muchos profesionales lo hacen. 🚶‍♂️ De hecho, probablemente estés aplicando patrones sin saberlo, guiado por intuición o experiencia. ¿Por qué entonces estudiarlos formalmente?

### Beneficios Concretos: 🔧

- **Conocimiento Probado** 💠 - Los patrones representan décadas de experiencia colectiva condensada en soluciones verificadas. Conocerlos te permite aprovechar este conocimiento acumulado sin tener que reinventar soluciones.

- **Vocabulario Común** 📝 - Frases como "Aquí aplicaría un Composite" o "Esto necesita un Mediator" comunican instantáneamente toda una estructura a otros desarrolladores familiarizados con patrones, facilitando la comunicación técnica en equipo.

Conocer patrones no es solo un ejercicio académico—es una herramienta práctica que mejora tu capacidad para resolver problemas y comunicarte efectivamente con otros profesionales. ⚡

## Clasificación de Patrones de Diseño 🗂️

Los patrones varían en escala y propósito, adaptándose a diferentes tipos de problemas. 🌳

Así como en literatura hay diferencia entre un poema corto y una novela extensa, los patrones también operan a diferentes escalas y con diferentes intenciones. 📝

### Niveles de Abstracción 📊

- **Idioms** (modismos): Son patrones de bajo nivel, generalmente específicos de un lenguaje de programación, que aprovechan características particulares para resolver problemas concretos de manera eficiente. 🔍

- **Patrones arquitectónicos**: En el otro extremo están estos patrones de alto nivel que pueden definir la estructura completa de una aplicación y son aplicables en prácticamente cualquier lenguaje de programación. 🏙️

### Categorías por Propósito 🎯

Los patrones también se clasifican según el tipo de problema que resuelven:

- **Patrones creacionales** 🌱: Manejan la creación de objetos de manera flexible, abstrayendo los detalles de instanciación y permitiendo decidir qué objetos crear en tiempo de ejecución.

- **Patrones estructurales** 🔄: Definen cómo combinar objetos y clases en estructuras más grandes manteniendo la flexibilidad y eficiencia. Establecen relaciones útiles entre componentes.

- **Patrones de comportamiento** 🤝: Gestionan la comunicación efectiva entre objetos, definiendo cómo interactúan y distribuyen responsabilidades para cumplir objetivos complejos.

Esta organización práctica nos ayuda a identificar rápidamente qué patrón podría ser útil según el tipo de problema que enfrentamos. 💡

# Patrones de Diseño en Golang: Pragmatismo y Elegancia 🧩

## La Relación entre Go y los Patrones de Diseño Clásicos ⚡

Golang emerge como un caso particular en el panorama de los lenguajes modernos. Creado en Google en 2009, ofrece un enfoque deliberadamente minimalista orientado a la construcción de sistemas distribuidos y servicios escalables. Su filosofía de diseño plantea un escenario interesante cuando se encuentra con los patrones establecidos en la década de los 90. 🔍

A diferencia de Java o C++, donde los patrones GoF encontraron su expresión original, Go adopta un enfoque estructural con interfaces implícitas y descarta intencionalmente la herencia de clases. Estas características fundamentales nos invitan a repensar cómo implementar los patrones tradicionales de manera idiomática en Go.

## Adaptación de Patrones al Estilo Go 🔄

La implementación de patrones en Go refleja las particularidades del lenguaje:

- **Composición sobre Herencia** 📦 - Go carece de herencia tradicional, favoreciendo en su lugar la composición de estructuras y el uso de interfaces. Esto altera significativamente la implementación de patrones como Decorator o Adapter.

- **Concurrencia Integrada** ⚙️ - Las goroutines y channels permiten implementaciones elegantes de patrones como Observer o Producer-Consumer, aprovechando las capacidades nativas del lenguaje.

- **Simplicidad y Pragmatismo** ✨ - El diseño de Go promueve soluciones directas y legibles, evitando abstracciones excesivamente complejas incluso cuando se implementan patrones sofisticados.

## El Balance entre Patrones y Estilo Idiomático 🌊

Para los desarrolladores de Go, existe una consideración constante entre aplicar patrones universales y mantener código que se siente natural en el ecosistema Go. ¿Cuándo implementar un Factory Method tradicional y cuándo utilizar simplemente funciones constructoras? ¿Es necesario un Singleton explícito cuando los packages de Go ya proporcionan un mecanismo similar?

Estas decisiones requieren comprender tanto los principios fundamentales de los patrones como las características específicas que Go ofrece para resolver problemas. El resultado ideal es código que aprovecha la sabiduría acumulada del diseño de software mientras respeta las fortalezas del lenguaje. 🧠

## Patrones como Herramientas, no como Reglas 🛠️

En el contexto de Go, los patrones funcionan mejor como conceptos compartidos que facilitan la comunicación sobre arquitectura, sin imponer implementaciones rígidas. Son herramientas de pensamiento que nos ayudan a estructurar soluciones, adaptándose a las particularidades del lenguaje.

Lo que veremos a continuación es cómo estos principios arquitectónicos encuentran su expresión en Go—un lenguaje que valora la claridad, la simplicidad y la eficiencia por encima de la complejidad abstracta. 💡

## Algunas notas antes de empezar 📝

- **Los patrones de diseño nacieron en el contexto OOP** 🧩

  - La mayoría de patrones clásicos fueron diseñados pensando en lenguajes orientados a objetos como Java o C++
  - Esto implica ciertas adaptaciones cuando los implementamos en Go

- **Go tiene un enfoque distinto al OOP tradicional** 🔄

  - No implementa herencia de clases (usa composición en su lugar)
  - Su modelo de encapsulación es más flexible que el tradicional
  - Las interfaces son implícitas, no requieren declaración explícita de implementación

- **El lenguaje tiene convenciones propias** 🔍

  - Las reglas de visibilidad se basan en mayúsculas/minúsculas (exportable o no exportable)
  - Favorece nombres concisos sobre descriptores verbosos
  - Promueve interfaces pequeñas y composición de comportamientos

- **Adaptaremos términos OOP al contexto de Go** 📚
  - Cuando hablemos de "jerarquías", nos referiremos a relaciones mediante interfaces compartidas o estructuras embebidas
  - Usaremos "propiedades" para referirnos a campos y sus métodos de acceso (getters/setters)
  - Mencionaremos "clases" aunque técnicamente Go usa structs con métodos asociados

Esta consciencia de las diferencias nos permitirá aplicar los patrones de forma idiomática, aprovechando las fortalezas de Go en lugar de forzar paradigmas ajenos al lenguaje. 🧠

## SOLID Design Principles en Go 🏗️

Antes de sumergirnos en patrones específicos, es fundamental comprender los principios SOLID—cinco reglas fundamentales que guían el diseño de software mantenible y escalable. 🧱 Estos principios, introducidos por Robert C. Martin ("Uncle Bob"), trascienden lenguajes específicos y proporcionan una base sólida para cualquier arquitectura de software.

En el contexto de Go, los principios SOLID adquieren matices interesantes. Aunque fueron concebidos para la programación orientada a objetos tradicional, su esencia se traduce perfectamente al enfoque más pragmático de Go. De hecho, algunas características del lenguaje—como sus interfaces implícitas y su énfasis en la composición—facilitan naturalmente la aplicación de ciertos principios SOLID. 🔄

Los principios SOLID (Responsabilidad Única, Abierto/Cerrado, Sustitución de Liskov, Segregación de Interfaces y Inversión de Dependencias) nos ayudan a crear código más adaptable, comprensible y testeable. No son reglas rígidas sino guías que, cuando se aplican con criterio, resultan en diseños más robustos que pueden evolucionar con menores fricciones. 🛠️

Veremos cómo estos principios cobran vida en Go, aprovechando las fortalezas del lenguaje para crear soluciones elegantes que mantienen la simplicidad característica de este lenguaje mientras construyen bases arquitectónicas sólidas. La implementación de SOLID en Go demuestra que estos principios son universales y adaptables, trascendiendo los paradigmas específicos de programación. 📐

- **S**: Single Responsibility Principle (SRP) - Principio de Responsabilidad Única
- **O**: Open/Closed Principle (OCP) - Principio Abierto/Cerrado
- **L**: Liskov Substitution Principle (LSP) - Principio de Sustitución de Liskov
- **I**: Interface Segregation Principle (ISP) - Principio de Segregación de Interfaces
- **D**: Dependency Inversion Principle (DIP) - Principio de Inversión de Dependencias

### Principio de Responsabilidad Única (SRP) 📜

El principio de responsabilidad única consiste en que cada función, clase o módulo debe tener una única razón de ser, es decir, debe ser creado con un único propósito/responsabilidad. Esto implica que el código de cada componente debe cambiar por una única razón relacionada con su propósito. En Go, este principio se aplica principalmente a funciones, structs y packages.

**❌ Violación del principio:**

```go
// Un struct con múltiples responsabilidades
type User struct {
    ID        int
    Name      string
    Email     string
    Password  string
}

func (u *User) Validate() bool {
    // Validación de datos del usuario
    return len(u.Name) > 0 && len(u.Email) > 0
}

func (u *User) Save() error {
    // Código para guardar el usuario en base de datos
    fmt.Println("Guardando usuario en base de datos...")
    return nil
}

func (u *User) SendWelcomeEmail() error {
    // Código para enviar email
    fmt.Printf("Enviando email de bienvenida a %s...\n", u.Email)
    return nil
}
```

**✅ Aplicando SRP:**

```go
// Modelo - Solo responsable de los datos
type User struct {
    ID       int
    Name     string
    Email    string
    Password string
}

// Validador - Responsable de validar datos
type UserValidator struct{}

func (v *UserValidator) Validate(user User) bool {
    return len(user.Name) > 0 && len(user.Email) > 0
}

// Repositorio - Responsable del almacenamiento
type UserRepository struct{}

func (r *UserRepository) Save(user User) error {
    fmt.Println("Guardando usuario en base de datos...")
    return nil
}

// Notificador - Responsable de las comunicaciones
type EmailService struct{}

func (e *EmailService) SendWelcomeEmail(user User) error {
    fmt.Printf("Enviando email de bienvenida a %s...\n", user.Email)
    return nil
}
```

Con esta separación, cada componente tiene una única razón para cambiar, facilitando el mantenimiento y las pruebas unitarias. 📋

### Principio Abierto/Cerrado (OCP) 🚪

Este principio establece que las entidades de software (clases, módulos, funciones) deben estar abiertas para extensión pero cerradas para modificación. Es decir, debemos poder añadir nuevas funcionalidades sin tener que modificar el código existente.

**❌ Violación del principio:**

```go
type Rectangle struct {
    Width, Height float64
}

type Circle struct {
    Radius float64
}

// Función que necesita modificarse cada vez que añadimos una nueva forma
func CalculateArea(shapes []interface{}) float64 {
    area := 0.0

    for _, shape := range shapes {
        switch s := shape.(type) {
        case Rectangle:
            area += s.Width * s.Height
        case Circle:
            area += math.Pi * s.Radius * s.Radius
        // Si añadimos un triángulo, necesitamos modificar esta función
        }
    }

    return area
}
```

**✅ Aplicando OCP:**

```go
// Interfaz común para todas las formas
type Shape interface {
    Area() float64
}

// Implementaciones concretas
type Rectangle struct {
    Width, Height float64
}

func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

type Circle struct {
    Radius float64
}

func (c Circle) Area() float64 {
    return math.Pi * c.Radius * c.Radius
}

// Función cerrada para modificación, abierta para extensión
func CalculateArea(shapes []Shape) float64 {
    area := 0.0
    for _, shape := range shapes {
        area += shape.Area()
    }
    return area
}

// Podemos añadir un nuevo tipo sin modificar código existente
type Triangle struct {
    Base, Height float64
}

func (t Triangle) Area() float64 {
    return 0.5 * t.Base * t.Height
}
```

Esta implementación permite añadir nuevas formas sin modificar la función `CalculateArea`. Las interfaces de Go son ideales para implementar este principio. 🧩

### Principio de Sustitución de Liskov (LSP) 🔄

Este principio establece que los objetos de un programa deberían ser reemplazables por instancias de sus subtipos sin alterar el correcto funcionamiento del programa. En Go, aunque no hay herencia tradicional, este principio se aplica a las relaciones entre interfaces y sus implementaciones.

**❌ Violación del principio:**

```go
type Bird interface {
    Fly()
    Sing()
}

type Sparrow struct{}

func (s *Sparrow) Fly() {
    fmt.Println("Volando a baja altura")
}

func (s *Sparrow) Sing() {
    fmt.Println("Pío pío")
}

type Penguin struct{}

// Un pingüino no vuela, pero debe implementar Fly() para cumplir con la interfaz
func (p *Penguin) Fly() {
    // Esto viola LSP porque cambia el comportamiento esperado
    panic("¡Los pingüinos no vuelan!")
}

func (p *Penguin) Sing() {
    fmt.Println("Cuack cuack")
}

// Esta función fallará con un pingüino
func MakeBirdFly(bird Bird) {
    bird.Fly()
}
```

**✅ Aplicando LSP:**

```go
// Interfaces más específicas
type Singer interface {
    Sing()
}

type Flyer interface {
    Fly()
}

// Ave genérica que canta
type Bird interface {
    Singer
}

// Ave voladora que también canta
type FlyingBird interface {
    Bird
    Flyer
}

// Implementaciones
type Sparrow struct{}

func (s *Sparrow) Fly() {
    fmt.Println("Volando a baja altura")
}

func (s *Sparrow) Sing() {
    fmt.Println("Pío pío")
}

type Penguin struct{}

func (p *Penguin) Sing() {
    fmt.Println("Cuack cuack")
}

// Funciones que respetan el principio LSP
func MakeBirdSing(bird Bird) {
    bird.Sing()  // Funciona con cualquier Bird
}

func MakeBirdFly(bird FlyingBird) {
    bird.Fly()  // Solo se usa con aves que pueden volar
}
```

Con este enfoque, las interfaces más específicas garantizan que sólo las aves que realmente pueden volar implementen `Flyer`. 🐦

### Principio de Segregación de Interfaces (ISP) 🧩

Este principio establece que ninguna clase debería ser forzada a depender de métodos que no usa. Es mejor tener muchas interfaces específicas que una interfaz general. Go, con su sistema de interfaces implícitas, favorece naturalmente este principio.

**❌ Violación del principio:**

```go
// Interfaz demasiado amplia
type Worker interface {
    Work()
    Eat()
    Sleep()
}

type Human struct{}

func (h *Human) Work() {
    fmt.Println("Trabajando...")
}

func (h *Human) Eat() {
    fmt.Println("Comiendo...")
}

func (h *Human) Sleep() {
    fmt.Println("Durmiendo...")
}

// Un robot puede trabajar pero no necesita comer ni dormir
type Robot struct{}

func (r *Robot) Work() {
    fmt.Println("Procesando tareas...")
}

func (r *Robot) Eat() {
    // Método vacío o innecesario
    fmt.Println("Los robots no comen")
}

func (r *Robot) Sleep() {
    // Método vacío o innecesario
    fmt.Println("Los robots no duermen")
}
```

**✅ Aplicando ISP:**

```go
// Interfaces segregadas y específicas
type Workable interface {
    Work()
}

type Eater interface {
    Eat()
}

type Sleeper interface {
    Sleep()
}

// Implementaciones
type Human struct{}

func (h *Human) Work() {
    fmt.Println("Trabajando...")
}

func (h *Human) Eat() {
    fmt.Println("Comiendo...")
}

func (h *Human) Sleep() {
    fmt.Println("Durmiendo...")
}

type Robot struct{}

func (r *Robot) Work() {
    fmt.Println("Procesando tareas...")
}

// Funciones que usan solo las interfaces necesarias
func DoWork(w Workable) {
    w.Work()
}

func HaveLunch(e Eater) {
    e.Eat()
}

func TakeRest(s Sleeper) {
    s.Sleep()
}
```

Las interfaces pequeñas y específicas permiten que los tipos implementen solo los comportamientos que realmente necesitan. En Go, este enfoque se considera idiomático. 🔍

### Principio de Inversión de Dependencias (DIP) 🔄

Este principio establece que los módulos de alto nivel no deben depender de los módulos de bajo nivel. Ambos deben depender de abstracciones. Además, las abstracciones no deben depender de los detalles, sino los detalles de las abstracciones.

**❌ Violación del principio:**

```go
// Módulo de bajo nivel
type MySQLDatabase struct{}

func (db *MySQLDatabase) Connect() {
    fmt.Println("Conectando a MySQL...")
}

func (db *MySQLDatabase) SaveData(data string) {
    fmt.Println("Guardando datos en MySQL:", data)
}

// Módulo de alto nivel depende directamente del módulo de bajo nivel
type UserService struct {
    database *MySQLDatabase
}

func NewUserService() *UserService {
    return &UserService{
        database: &MySQLDatabase{},
    }
}

func (s *UserService) CreateUser(userData string) {
    s.database.Connect()
    s.database.SaveData(userData)
}
```

**✅ Aplicando DIP:**

```go
// Abstracción
type Database interface {
    Connect()
    SaveData(data string)
}

// Implementación de bajo nivel
type MySQLDatabase struct{}

func (db *MySQLDatabase) Connect() {
    fmt.Println("Conectando a MySQL...")
}

func (db *MySQLDatabase) SaveData(data string) {
    fmt.Println("Guardando datos en MySQL:", data)
}

// Implementación alternativa
type PostgresDatabase struct{}

func (db *PostgresDatabase) Connect() {
    fmt.Println("Conectando a PostgreSQL...")
}

func (db *PostgresDatabase) SaveData(data string) {
    fmt.Println("Guardando datos en PostgreSQL:", data)
}

// Módulo de alto nivel depende de una abstracción
type UserService struct {
    database Database
}

// Inyección de dependencia
func NewUserService(db Database) *UserService {
    return &UserService{
        database: db,
    }
}

func (s *UserService) CreateUser(userData string) {
    s.database.Connect()
    s.database.SaveData(userData)
}

// Uso
func main() {
    mysqlDB := &MySQLDatabase{}
    service := NewUserService(mysqlDB)
    service.CreateUser("John Doe")

    // Fácilmente podemos cambiar la implementación
    postgresDB := &PostgresDatabase{}
    service = NewUserService(postgresDB)
    service.CreateUser("Jane Doe")
}
```

Mediante la inversión de dependencias, el módulo de alto nivel (`UserService`) ahora depende de una abstracción (`Database`), no de una implementación concreta. Esto mejora la flexibilidad y facilita las pruebas. 🧪

Los principios SOLID en Go aprovechan las características del lenguaje, como interfaces implícitas y composición, para crear código más mantenible, extensible y testeable. Siguiendo estos principios, construirás sistemas robustos que pueden evolucionar con menores fricciones. 🚀

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

# Factory Pattern 🏭

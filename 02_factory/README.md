# Factory Pattern 🏭

## ¿Qué es el Factory Pattern? 🤔

El **Factory Pattern** es un patrón de diseño creacional que proporciona una interfaz para crear objetos sin especificar sus clases concretas. Mientras que el Builder Pattern se enfoca en construir objetos complejos paso a paso, el Factory se especializa en la creación directa de objetos relacionados con una configuración adecuada. 🛠️

Este patrón es especialmente útil cuando:

- La creación de objetos requiere lógica que no pertenece al constructor
- Necesitas encapsular la lógica de instanciación
- Quieres centralizar la validación y configuración de objetos
- Deseas desacoplar el código cliente de las clases concretas

## Tipos de Factory Pattern 📋

### 1. Simple Factory 🔨

El más básico de los patrones factory - una función o método que crea y retorna instancias:

```go
package main

import "fmt"

// Struct que queremos instanciar de manera controlada
type Person struct {
    Name     string
    Age      int
    EyeCount int
}

// Simple Factory con validaciones integradas
func NewPerson(name string, age int) *Person {
    // Validaciones de negocio centralizadas
    if age < 0 {
        panic("La edad no puede ser negativa")
    }
    if name == "" {
        panic("El nombre no puede estar vacío")
    }

    // Creación con valores por defecto y configuración adecuada
    return &Person{
        Name:     name,
        Age:      age,
        EyeCount: 2, // Valor predeterminado lógico
    }
}

func main() {
    // Uso sencillo - el cliente no necesita conocer detalles de inicialización
    p := NewPerson("John", 30)

    // Posibilidad de modificar después de la creación si es necesario
    p.EyeCount = 1

    fmt.Printf("%+v\n", p) // {Name:John Age:30 EyeCount:1}
}
```

### 2. Factory Method Pattern 🏗️

Este patrón define una interfaz para crear objetos, pero permite a las subclases decidir qué clase instanciar:

```go
package main

import "fmt"

// Interfaz del producto
type PaymentMethod interface {
    Pay(amount float64) string
}

// Implementaciones concretas
type CreditCardPayment struct {
    cardNumber string
}

func (c *CreditCardPayment) Pay(amount float64) string {
    return fmt.Sprintf("Pagando %.2f con tarjeta %s", amount, c.cardNumber)
}

type PayPalPayment struct {
    email string
}

func (p *PayPalPayment) Pay(amount float64) string {
    return fmt.Sprintf("Pagando %.2f con PayPal account %s", amount, p.email)
}

// Factory que crea diferentes métodos de pago
type PaymentFactory struct{}

func (f *PaymentFactory) CreatePayment(method string, details string) (PaymentMethod, error) {
    switch method {
    case "creditcard":
        return &CreditCardPayment{cardNumber: details}, nil
    case "paypal":
        return &PayPalPayment{email: details}, nil
    default:
        return nil, fmt.Errorf("método de pago no soportado: %s", method)
    }
}

func main() {
    factory := &PaymentFactory{}

    // El cliente trabaja con la abstracción PaymentMethod
    creditCardPayment, _ := factory.CreatePayment("creditcard", "1234-5678-9012-3456")
    fmt.Println(creditCardPayment.Pay(100.50))

    paypalPayment, _ := factory.CreatePayment("paypal", "usuario@ejemplo.com")
    fmt.Println(paypalPayment.Pay(50.75))
}
```

## Beneficios del Factory Pattern 🌟

1. **Encapsulación de la creación**: Oculta la lógica de instanciación y configuración ✅
2. **Centraliza la validación**: Todas las reglas de negocio para crear objetos válidos están en un solo lugar 📝
3. **Facilita cambios**: Puedes modificar los detalles de implementación sin afectar el código cliente 🔄
4. **Reutilización de código**: Evita la duplicación de lógica de inicialización 🔁
5. **Mejora la legibilidad**: El nombre del factory comunica claramente su propósito (`NewPerson`, `CreatePayment`) 📚

## Cuándo Usar Factory en Go 🧩

El patrón Factory es particularmente útil en Go cuando:

- Trabajas con estructuras complejas que requieren inicialización específica
- Necesitas aplicar reglas de negocio durante la creación de objetos
- Quieres proporcionar una API clara para la creación de objetos
- Implementas sistemas con múltiples implementaciones intercambiables de interfaces
- Buscas gestionar la creación de objetos en un ecosistema de microservicios

A diferencia del Builder que brilla en la construcción paso a paso de objetos complejos, el Factory Pattern destaca cuando necesitas una forma concisa y directa de crear objetos correctamente configurados con una sola llamada de función. 🚀

## Interface Factory: Abstraer la Implementación 🎭

Un poderoso enfoque dentro del patrón Factory es retornar interfaces en lugar de implementaciones concretas. Esta técnica permite desacoplar completamente el código cliente de los detalles de implementación, siguiendo el principio de "programar hacia interfaces, no hacia implementaciones". 🧩

### ¿Por qué retornar interfaces? 🤔

Cuando una factory devuelve una interfaz en lugar de un tipo concreto:

- El cliente no puede acceder a detalles de implementación que no deberían ser públicos
- La implementación puede cambiarse o extenderse sin afectar a los clientes existentes
- Facilita considerablemente las pruebas unitarias mediante mocks
- Refuerza los principios de diseño SOLID, especialmente la Inversión de Dependencias

### Implementación en Go 💻

```go
package main

import "fmt"

// Interfaz pública que define el comportamiento
type Person interface {
  SayHello()
  Age() int  // Método getter que expone solo lo necesario
}

// Implementación privada (minúscula inicial)
type person struct {
  name string
  age  int
  // Podríamos tener muchos más campos internos
  // que no queremos exponer al exterior
  internalID    string
  securityLevel int
  preferences   map[string]string
}

// Implementación de los métodos de la interfaz
func (p *person) SayHello() {
  fmt.Printf("Hola, soy %s y tengo %d años\n", p.name, p.age)
}

func (p *person) Age() int {
  return p.age  // Acceso controlado a los datos
}

// Factory que retorna la interfaz en lugar del tipo concreto
func NewPerson(name string, age int) Person {
  // Podemos inicializar campos privados complejos sin exponerlos
  return &person{
    name:          name,
    age:           age,
    internalID:    generateID(name),  // Función ficticia
    securityLevel: determineLevel(),  // Función ficticia
    preferences:   defaultPreferences(),  // Función ficticia
  }
}

// Funciones ficticias para el ejemplo
func generateID(name string) string {
  return "ID-" + name
}

func determineLevel() int {
  return 2
}

func defaultPreferences() map[string]string {
  return map[string]string{"theme": "dark", "notifications": "enabled"}
}

func main() {
  // El cliente trabaja exclusivamente con la interfaz
  p := NewPerson("John", 30)
  p.SayHello()  // Salida: Hola, soy John y tengo 30 años

  fmt.Printf("La persona tiene %d años\n", p.Age())

  // No es posible:
  // fmt.Println(p.name)             // Error: p.name no es accesible
  // p.preferences["theme"] = "light" // Error: p.preferences no es accesible
}
```

### Beneficios de Interface Factory 🌟

1. **Encapsulación mejorada** 🔒 - Los clientes no pueden modificar propiedades internas ni acceder a detalles de implementación

2. **Evolución sin fricción** 🔄 - La implementación puede cambiar completamente mientras se mantenga la interfaz:

   ```go
   // En una actualización futura podríamos hacer esto:
   func NewPerson(name string, age int) Person {
     // Cambio completo de implementación sin afectar a los clientes
     return &enhancedPerson{
       userData: &userData{name: name, age: age},
       analytics: newAnalyticsTracker(),
     }
   }
   ```

3. **API minimalista** 📝 - Expone solo las operaciones esenciales, simplificando el uso para los clientes

4. **Pruebas simplificadas** 🧪 - Facilita la creación de implementaciones mock para testing:

   ```go
   type MockPerson struct{}

   func (m *MockPerson) SayHello() { fmt.Println("Mock hello") }
   func (m *MockPerson) Age() int { return 42 }

   func TestWithMockPerson(t *testing.T) {
     p := &MockPerson{}
     // Probar código que utiliza Person sin necesidad de crear personas reales
   }
   ```

### Consideraciones de Diseño 🧐

- Defina interfaces **pequeñas y cohesivas** que representen capacidades específicas
- No exponga detalles internos a través de la interfaz
- Considere usar múltiples interfaces pequeñas en lugar de una grande (ISP: Interface Segregation Principle)
- Utilice nombres descriptivos para las interfaces (`Reader`, `Writer`, `Closer` en lugar de `ReaderInterface`)

Este patrón es una herramienta fundamental en Go para crear sistemas flexibles, mantenibles y testables, aprovechando al máximo el sistema de interfaces implícitas del lenguaje. 🚀

## Factory Generator: Creando Factories a Medida 🏭

Un **Factory Generator** es un patrón avanzado que nos permite crear factories personalizadas dinámicamente. En lugar de codificar una función factory para cada variante de un objeto, creamos un generador que produce factories especializadas según parámetros configurables. Este enfoque es particularmente valioso cuando necesitamos múltiples factories con configuraciones similares pero distintas. 🧰

### Enfoque Funcional: Closures como Factories 🧩

El enfoque funcional aprovecha las closures de Go para "recordar" valores preconfigurados:

```go
package main

import "fmt"

type Employee struct {
    Name, Position string
    AnnualIncome int
}

// Factory Generator - Una función que devuelve otra función (factory)
func NewEmployeeFactory(position string, annualIncome int) func(name string) *Employee {
  // La closure "recuerda" position y annualIncome
  return func(name string) *Employee {
    // Cada llamada crea un Employee con los valores preconfigurados
    return &Employee{
      Name: name,
      Position: position,
      AnnualIncome: annualIncome,
    }
  }
}

func main() {
  // Creamos factories especializadas con configuración predefinida
  developerFactory := NewEmployeeFactory("Developer", 100000)
  managerFactory := NewEmployeeFactory("Manager", 150000)

  // Usamos cada factory para crear instancias específicas
  developer := developerFactory("Alice")  // Solo necesitamos proporcionar el nombre
  manager := managerFactory("Bob")

  fmt.Println(developer) // {Alice Developer 100000}
  fmt.Println(manager)   // {Bob Manager 150000}

  // Podemos pasar estas factories como argumentos a otras funciones
  createTeam(developerFactory, 5)  // Crear 5 desarrolladores
}

// Ejemplo de función que acepta una factory como parámetro
func createTeam(factory func(string) *Employee, count int) []*Employee {
  team := make([]*Employee, count)
  for i := 0; i < count; i++ {
    team[i] = factory(fmt.Sprintf("Employee-%d", i+1))
  }
  return team
}
```

### Enfoque Estructurado: Factories como Objetos 🏛️

El enfoque estructurado encapsula la configuración en un objeto factory:

```go
package main

import "fmt"

type Employee struct {
    Name, Position string
    AnnualIncome int
}

// La factory como estructura que almacena configuración
type EmployeeFactory struct {
    Position string
    AnnualIncome int
}

// Método para crear empleados con la configuración de la factory
func (f *EmployeeFactory) Create(name string) *Employee {
    return &Employee{
        Name: name,
        Position: f.Position,
        AnnualIncome: f.AnnualIncome,
    }
}

// Podemos añadir métodos adicionales a la factory
func (f *EmployeeFactory) CreateWithBonus(name string, bonusPercent float64) *Employee {
    employee := f.Create(name)
    employee.AnnualIncome += int(float64(employee.AnnualIncome) * bonusPercent)
    return employee
}

// Factory generator para crear factories configuradas
func NewEmployeeFactory(position string, annualIncome int) *EmployeeFactory {
    return &EmployeeFactory{
        Position: position,
        AnnualIncome: annualIncome,
    }
}

func main() {
    // Creamos factories especializadas
    developerFactory := NewEmployeeFactory("Developer", 100000)
    managerFactory := NewEmployeeFactory("Manager", 150000)

    // Usamos los métodos de la factory para crear instancias
    developer := developerFactory.Create("Alice")
    manager := managerFactory.Create("Bob")

    // Podemos usar métodos adicionales de la factory
    seniorDev := developerFactory.CreateWithBonus("Charlie", 0.1) // 10% bonus

    fmt.Println(developer)  // {Alice Developer 100000}
    fmt.Println(manager)    // {Bob Manager 150000}
    fmt.Println(seniorDev)  // {Charlie Developer 110000}
}
```

### ¿Cuál enfoque elegir? 🤔

**Enfoque funcional** es ideal cuando:

- Necesitas factories ligeras y minimalistas
- Quieres pasar las factories como argumentos a otras funciones
- Prefieres un estilo de programación más funcional

**Enfoque estructurado** brilla cuando:

- Necesitas métodos adicionales en tus factories (como validaciones o variantes de creación)
- La factory requiere su propio estado o comportamiento complejo
- Prefieres APIs orientadas a objetos con métodos descriptivos

Ambos enfoques son válidos en Go, y la elección depende principalmente de tu estilo de programación y las necesidades específicas de tu aplicación. El patrón Factory Generator, independientemente del enfoque, permite crear una familia de factories especializadas que comparten estructura pero difieren en configuración, reduciendo la duplicación de código. 🚀

## Prototype Factory: Clonación en Lugar de Construcción 🧬

El **Prototype Factory** combina los patrones Factory y Prototype para crear objetos a partir de plantillas predefinidas. En lugar de construir objetos desde cero cada vez, este patrón mantiene instancias prototípicas que pueden clonarse para crear nuevos objetos. Esta estrategia es particularmente valiosa cuando:

- La creación de un objeto implica operaciones costosas (acceso a bases de datos, cálculos complejos)
- Necesitas muchas variantes de objetos que difieren solo en algunos valores
- Quieres evitar jerarquías de clases factory para cada tipo de objeto
- Las configuraciones iniciales son complejas pero se repiten frecuentemente

### Implementación Básica 🔍

```go
package main

import "fmt"

type Employee struct {
    Name, Position string
    AnnualIncome int
}

// Constantes para roles predefinidos
const (
    Developer = iota  // 0
    Manager           // 1
)

// Factory que retorna prototipos según el rol solicitado
func NewEmployee(role int) *Employee {
    // Prototipos predefinidos según el rol
    switch role {
        case Developer:
            return &Employee{"", "Developer", 100000}  // Prototipo para desarrollador
        case Manager:
            return &Employee{"", "Manager", 150000}    // Prototipo para gerente
        default:
            panic("Rol no soportado")
    }
}

func main() {
    // Obtenemos un prototipo de Manager
    m := NewEmployee(Manager)
    // Personalizamos solo lo necesario (el nombre)
    m.Name = "Alice"
    fmt.Println(m) // {Alice Manager 150000}

    // Podemos crear múltiples objetos del mismo tipo
    d1 := NewEmployee(Developer)
    d1.Name = "Bob"

    d2 := NewEmployee(Developer)
    d2.Name = "Charlie"

    fmt.Println(d1) // {Bob Developer 100000}
    fmt.Println(d2) // {Charlie Developer 100000}
}
```

### Implementación Avanzada con Clonación Explícita 🧪

Una implementación más robusta incluye métodos de clonación explícitos:

```go
package main

import "fmt"

// Interfaz para objetos clonables
type Prototype interface {
    Clone() Prototype
    GetInfo() string
}

// Implementación concreta: Employee
type Employee struct {
    Name, Position string
    AnnualIncome   int
    Skills         []string  // Campo complejo (slice)
}

// Implementación del método Clone()
func (e *Employee) Clone() Prototype {
    // Copia profunda - importante para estructuras con campos complejos
    skillsCopy := make([]string, len(e.Skills))
    copy(skillsCopy, e.Skills)

    return &Employee{
        Name:         e.Name,
        Position:     e.Position,
        AnnualIncome: e.AnnualIncome,
        Skills:       skillsCopy,
    }
}

func (e *Employee) GetInfo() string {
    return fmt.Sprintf("%s - %s ($%d)", e.Name, e.Position, e.AnnualIncome)
}

// PrototypeRegistry mantiene un registro de prototipos disponibles
type PrototypeRegistry struct {
    prototypes map[string]Prototype
}

func NewPrototypeRegistry() *PrototypeRegistry {
    return &PrototypeRegistry{
        prototypes: make(map[string]Prototype),
    }
}

// Registra un prototipo con un identificador
func (r *PrototypeRegistry) Register(name string, prototype Prototype) {
    r.prototypes[name] = prototype
}

// Crea un clon a partir de un prototipo registrado
func (r *PrototypeRegistry) Create(name string) Prototype {
    if prototype, ok := r.prototypes[name]; ok {
        return prototype.Clone()
    }
    return nil
}

func main() {
    // Crear el registro de prototipos
    registry := NewPrototypeRegistry()

    // Registrar prototipos base
    registry.Register("developer", &Employee{
        Position:     "Developer",
        AnnualIncome: 100000,
        Skills:       []string{"Go", "SQL", "JavaScript"},
    })

    registry.Register("manager", &Employee{
        Position:     "Manager",
        AnnualIncome: 150000,
        Skills:       []string{"Leadership", "Communication", "Planning"},
    })

    // Crear instancias basadas en prototipos
    dev1 := registry.Create("developer").(*Employee)
    dev1.Name = "Alice"
    dev1.Skills = append(dev1.Skills, "Rust") // Modificamos solo este clon

    dev2 := registry.Create("developer").(*Employee)
    dev2.Name = "Bob"

    mgr := registry.Create("manager").(*Employee)
    mgr.Name = "Charlie"

    // Verificar que tenemos copias independientes
    fmt.Println(dev1.GetInfo())  // Alice - Developer ($100000)
    fmt.Println(dev2.GetInfo())  // Bob - Developer ($100000)
    fmt.Println(mgr.GetInfo())   // Charlie - Manager ($150000)

    fmt.Println("Dev1 skills:", dev1.Skills) // [Go SQL JavaScript Rust]
    fmt.Println("Dev2 skills:", dev2.Skills) // [Go SQL JavaScript]
}
```

### Ventajas del Prototype Factory 💪

1. **Rendimiento mejorado**: Clonar objetos suele ser más eficiente que crearlos desde cero, especialmente para objetos complejos 🚀

2. **Reducción de código repetitivo**: Define un objeto base una vez y luego haz pequeñas modificaciones 📝

3. **Creación dinámica**: Puedes añadir y eliminar prototipos en tiempo de ejecución según las necesidades 🔄

4. **Encapsulación de complejidad**: Los clientes no necesitan conocer cómo se construyen los objetos, solo clonan prototipos existentes ✨

5. **Preservación del estado**: Puedes crear prototipos que ya contengan un estado específico, especialmente útil para objetos con configuraciones complejas 🧠

Esta combinación de Factory y Prototype ofrece una forma flexible y eficiente de crear objetos con características compartidas, permitiendo personalizaciones específicas después de la clonación. 🧩

## Sumario 📝

- Una función factory (a.k.a. constructor) es una función helper que crea y retorna instancias de un tipo específico, encapsulando la lógica de inicialización y validación.
- Un factory puede ser cualquier entidad que produzca instancias de un tipo, ya sea una función, un método o una estructura.
- Puede ser una función simple, un método de una estructura o una interfaz que define un contrato para crear instancias.

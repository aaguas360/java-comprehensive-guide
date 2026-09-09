# PATRONES DE DISEÑO EN JAVA

## Índice (Tabla de contenidos)
1. [Introducción](#1-introducción)
2. [Mapa rápido de patrones](#2-mapa-rápido-de-patrones)
3. [Patrones creacionales](#3-patrones-creacionales)
4. [Patrones estructurales](#4-patrones-estructurales)
5. [Patrones de comportamiento](#5-patrones-de-comportamiento)
6. [Comparativas y decisiones de diseño](#6-comparativas-y-decisiones-de-diseño)
7. [Conclusiones y recomendaciones](#7-conclusiones-y-recomendaciones)

---

## 1. Introducción

Este documento especializa el uso de patrones en Java con enfoque práctico empresarial.

Diagrama conceptual:

```text
Problema repetido -> Patrón adecuado -> Implementación Java -> Pruebas -> Evolución
```

---

## 2. Mapa rápido de patrones

| Categoría | Patrones |
|---|---|
| Creacionales | Singleton, Factory, Builder |
| Estructurales | Decorator, Adapter, Proxy |
| Comportamiento | Strategy, Observer, Command, Template Method, State, Chain of Responsibility, Mediator, Memento, Iterator, Visitor |

---

## 3. Patrones creacionales

### 3.1 Singleton
1. **Definición técnica:** Garantiza una sola instancia global con acceso controlado.
2. **Definición sencilla:** Un único objeto compartido por toda la app.
3. **Problema que resuelve:** Evitar múltiples instancias de un recurso central.
4. **Ejemplo Java completo:**
```java
public final class ConfigSingleton {
    private static final ConfigSingleton INSTANCE = new ConfigSingleton();

    private ConfigSingleton() {}

    public static ConfigSingleton getInstance() {
        return INSTANCE;
    }

    public String appName() {
        return "java-guide";
    }
}
```
5. **Explicación detallada:** constructor privado evita `new`; instancia eager thread-safe por classloader.
6. **Caso empresarial:** Configuración global de aplicación.
7. **Ventajas/desventajas:** simple y rápido / puede dificultar testabilidad.
8. **Variaciones/alternativas:** enum singleton, DI container.

### 3.2 Factory Method
1. Definición técnica: Encapsula creación delegándola a factoría.
2. Definición sencilla: Una “fábrica” decide qué objeto crear.
3. Problema: Evitar `new` dispersos y condicionales por tipo.
4. Ejemplo Java:
```java
interface Reporte { String generar(); }
class ReportePdf implements Reporte { public String generar() { return "PDF"; } }
class ReporteCsv implements Reporte { public String generar() { return "CSV"; } }

class ReporteFactory {
    static Reporte crear(String tipo) {
        return switch (tipo) {
            case "PDF" -> new ReportePdf();
            case "CSV" -> new ReporteCsv();
            default -> throw new IllegalArgumentException("Tipo no soportado");
        };
    }
}
```
5. Explicación: centraliza la creación y protege al consumidor.
6. Caso real: Exportación multiformato.
7. Ventajas/desventajas: extensible / fábrica puede crecer demasiado.
8. Alternativas: Abstract Factory, Strategy + registro.

### 3.3 Builder
1. Definición técnica: Construcción paso a paso de objetos complejos.
2. Definición sencilla: Armar objeto como un “combo configurable”.
3. Problema: constructores telescópicos.
4. Ejemplo Java:
```java
class Usuario {
    private final String id;
    private final String nombre;
    private final String email;

    private Usuario(Builder b) {
        this.id = b.id;
        this.nombre = b.nombre;
        this.email = b.email;
    }

    static class Builder {
        private String id;
        private String nombre;
        private String email;

        Builder id(String id) { this.id = id; return this; }
        Builder nombre(String nombre) { this.nombre = nombre; return this; }
        Builder email(String email) { this.email = email; return this; }
        Usuario build() { return new Usuario(this); }
    }
}
```
5. Explicación: objeto inmutable construido fluido.
6. Caso real: DTOs de onboarding.
7. Ventajas/desventajas: legible / más código boilerplate.
8. Alternativas: record + factories.

---

## 4. Patrones estructurales

### 4.1 Decorator
1. Definición técnica: Añade comportamiento dinámico envolviendo objeto.
2. Definición sencilla: “Capas” de funcionalidades.
3. Problema: Evitar explosión de subclases.
4. Ejemplo Java:
```java
interface Mensaje { String contenido(); }
class MensajeBase implements Mensaje { public String contenido() { return "Hola"; } }
class FirmaDecorator implements Mensaje {
    private final Mensaje inner;
    FirmaDecorator(Mensaje inner) { this.inner = inner; }
    public String contenido() { return inner.contenido() + "\n-- Equipo"; }
}
```
5. Explicación: composición para extender sin modificar.
6. Caso real: pipelines de notificación.
7. Ventajas/desventajas: flexible / trazabilidad más compleja.
8. Alternativas: AOP, interceptores.

### 4.2 Adapter
1. Definición técnica: Convierte interfaz incompatible en otra esperada.
2. Definición sencilla: “Traductor” entre dos sistemas.
3. Problema: Integrar APIs legacy.
4. Ejemplo Java:
```java
interface PagoNuevo { void pagar(double monto); }
class PagoLegacy { void makePayment(double amount) { System.out.println("Legacy " + amount); } }
class PagoAdapter implements PagoNuevo {
    private final PagoLegacy legacy = new PagoLegacy();
    public void pagar(double monto) { legacy.makePayment(monto); }
}
```
5. Explicación: encapsula compatibilidad en un solo punto.
6. Caso real: conexión con proveedor antiguo.
7. Ventajas/desventajas: desacopla migraciones / capa adicional.
8. Alternativas: Facade, Anti-corruption layer.

### 4.3 Proxy
1. Definición técnica: Sustituto que controla acceso a objeto real.
2. Definición sencilla: Portero antes de entrar al servicio real.
3. Problema: control de acceso, caché o lazy loading.
4. Ejemplo Java:
```java
interface DocumentoService { String leer(String id); }
class DocumentoReal implements DocumentoService {
    public String leer(String id) { return "Documento " + id; }
}
class DocumentoProxy implements DocumentoService {
    private final DocumentoService real = new DocumentoReal();
    public String leer(String id) {
        if (!id.startsWith("DOC-")) throw new SecurityException("No autorizado");
        return real.leer(id);
    }
}
```
5. Explicación: proxy valida y delega.
6. Caso real: API Gateway interno.
7. Ventajas/desventajas: seguridad transversal / sobrecarga ligera.
8. Alternativas: filtros HTTP, interceptores.

---

## 5. Patrones de comportamiento

### 5.1 Strategy
1. **Definición técnica:** Encapsula algoritmos intercambiables detrás de una interfaz común.
2. **Definición sencilla:** Cambiar la forma de resolver algo sin tocar el cliente.
3. **Problema que resuelve:** Evitar `if/else` por tipo de comportamiento.
4. **Ejemplo Java completo:**
```java
interface PrecioStrategy { double aplicar(double base); }
class PrecioNormal implements PrecioStrategy { public double aplicar(double base) { return base; } }
class PrecioPromo implements PrecioStrategy { public double aplicar(double base) { return base * 0.85; } }
class Carrito {
    private final PrecioStrategy strategy;
    Carrito(PrecioStrategy strategy) { this.strategy = strategy; }
    double total(double base) { return strategy.aplicar(base); }
}
```
5. **Explicación detallada:** El algoritmo variable queda aislado y reemplazable en runtime.
6. **Caso de uso empresarial:** Promociones por canal de venta.
7. **Ventajas/desventajas:** extensible y testeable / más clases.
8. **Variaciones/alternativas:** Policy objects, funciones lambda.

### 5.2 Observer
1. **Definición técnica:** Relación uno-a-muchos con notificación ante cambios del sujeto.
2. **Definición sencilla:** Los suscriptores reciben avisos automáticos.
3. **Problema que resuelve:** Comunicación desacoplada de eventos.
4. **Ejemplo Java completo:**
```java
import java.util.*;
interface Observer { void update(String evento); }
class Topic {
    private final List<Observer> observers = new ArrayList<>();
    void subscribe(Observer o) { observers.add(o); }
    void publish(String evento) { observers.forEach(o -> o.update(evento)); }
}
```
5. **Explicación detallada:** `Topic` mantiene observadores y emite eventos sin conocer implementaciones.
6. **Caso de uso empresarial:** Alertas de estado de pedidos.
7. **Ventajas/desventajas:** bajo acoplamiento / difícil depurar secuencia de eventos.
8. **Variaciones/alternativas:** Event bus, pub/sub con broker.

### 5.3 Command
1. **Definición técnica:** Encapsula una solicitud como objeto ejecutable.
2. **Definición sencilla:** Guardar una acción para ejecutarla después.
3. **Problema que resuelve:** Desacoplar quien pide de quien ejecuta.
4. **Ejemplo Java completo:**
```java
interface Command { void execute(); }
class GenerarFacturaCommand implements Command {
    public void execute() { System.out.println("Factura generada"); }
}
class Invoker {
    void run(Command command) { command.execute(); }
}
```
5. **Explicación detallada:** `Invoker` solo conoce el contrato `Command`.
6. **Caso de uso empresarial:** Colas de tareas, retry y auditoría.
7. **Ventajas/desventajas:** serializable y trazable / más objetos.
8. **Variaciones/alternativas:** Job queues, eventos de dominio.

### 5.4 Template Method
1. **Definición técnica:** Define esqueleto de algoritmo delegando pasos variables a subclases.
2. **Definición sencilla:** Flujo fijo con piezas reemplazables.
3. **Problema que resuelve:** Repetir procesos iguales con pequeñas variaciones.
4. **Ejemplo Java completo:**
```java
abstract class ProcesoCierre {
    final void ejecutar() { validar(); persistir(); notificar(); }
    abstract void validar();
    abstract void persistir();
    void notificar() { System.out.println("Notificado"); }
}
```
5. **Explicación detallada:** método `final` protege orden y subclases completan pasos.
6. **Caso de uso empresarial:** Cierre diario por país.
7. **Ventajas/desventajas:** consistencia de flujo / herencia rígida.
8. **Variaciones/alternativas:** Strategy + composición.

### 5.5 State
1. **Definición técnica:** Representa estados como objetos con comportamiento propio.
2. **Definición sencilla:** El objeto actúa distinto según su estado.
3. **Problema que resuelve:** `switch` gigantes por estado.
4. **Ejemplo Java completo:**
```java
interface EstadoPedido { String avanzar(); }
class Creado implements EstadoPedido { public String avanzar() { return "PAGADO"; } }
class Pagado implements EstadoPedido { public String avanzar() { return "ENVIADO"; } }
```
5. **Explicación detallada:** cada estado encapsula transición y reglas.
6. **Caso de uso empresarial:** Workflow de pedido.
7. **Ventajas/desventajas:** claridad del ciclo de vida / más clases.
8. **Variaciones/alternativas:** máquinas de estado externas.

### 5.6 Chain of Responsibility
1. **Definición técnica:** Encadena manejadores que procesan o delegan solicitud.
2. **Definición sencilla:** Filtros en secuencia.
3. **Problema que resuelve:** Acoplar validaciones en un método único.
4. **Ejemplo Java completo:**
```java
interface Handler { boolean handle(String v); }
class NoNulo implements Handler { public boolean handle(String v) { return v != null; } }
class NoVacio implements Handler { public boolean handle(String v) { return !v.isBlank(); } }
```
5. **Explicación detallada:** cada handler cumple una regla independiente.
6. **Caso de uso empresarial:** Validación de formularios.
7. **Ventajas/desventajas:** extensible / orden de cadena importa.
8. **Variaciones/alternativas:** pipeline funcional.

### 5.7 Mediator
1. **Definición técnica:** Objeto central coordina colaboración entre componentes.
2. **Definición sencilla:** Un “controlador” evita que todos hablen con todos.
3. **Problema que resuelve:** Dependencias cruzadas difíciles de mantener.
4. **Ejemplo Java completo:**
```java
interface ChatMediator { void send(String msg, UsuarioChat from); }
class UsuarioChat {
    private final ChatMediator mediator;
    UsuarioChat(ChatMediator mediator) { this.mediator = mediator; }
    void enviar(String msg) { mediator.send(msg, this); }
}
```
5. **Explicación detallada:** los colegas se comunican solo vía mediador.
6. **Caso de uso empresarial:** Orquestación de módulos UI.
7. **Ventajas/desventajas:** baja complejidad entre colegas / mediador puede crecer.
8. **Variaciones/alternativas:** Event bus.

### 5.8 Memento
1. **Definición técnica:** Captura estado interno sin violar encapsulamiento.
2. **Definición sencilla:** Guardar “snapshot” para deshacer.
3. **Problema que resuelve:** Recuperación ante cambios erróneos.
4. **Ejemplo Java completo:**
```java
class Editor {
    private String texto = "";
    void escribir(String t) { texto = t; }
    String save() { return texto; }
    void restore(String snapshot) { texto = snapshot; }
}
```
5. **Explicación detallada:** snapshot externo restaura estado previo.
6. **Caso de uso empresarial:** Edición de plantillas.
7. **Ventajas/desventajas:** soporte undo / consumo de memoria.
8. **Variaciones/alternativas:** event sourcing parcial.

### 5.9 Iterator
1. **Definición técnica:** Provee acceso secuencial a elementos sin exponer implementación interna.
2. **Definición sencilla:** Recorrer datos sin saber cómo están guardados.
3. **Problema que resuelve:** Acoplamiento al tipo de colección.
4. **Ejemplo Java completo:**
```java
java.util.Iterator<Integer> it = java.util.List.of(1, 2, 3).iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```
5. **Explicación detallada:** contrato uniforme de recorrido con `hasNext/next`.
6. **Caso de uso empresarial:** Lectura paginada de resultados.
7. **Ventajas/desventajas:** encapsulación / poca lógica de negocio.
8. **Variaciones/alternativas:** streams y for-each.

### 5.10 Visitor
1. **Definición técnica:** Separa operaciones de la estructura de objetos visitados.
2. **Definición sencilla:** Agregar comportamientos nuevos sin tocar las clases base.
3. **Problema que resuelve:** Cambios frecuentes de operaciones sobre objetos estables.
4. **Ejemplo Java completo:**
```java
interface Nodo { void accept(Visitor v); }
class NodoTexto implements Nodo {
    private final String value;
    NodoTexto(String value) { this.value = value; }
    public void accept(Visitor v) { v.visit(this); }
    String value() { return value; }
}
interface Visitor { void visit(NodoTexto nodo); }
```
5. **Explicación detallada:** doble despacho para aplicar lógica externa al objeto.
6. **Caso de uso empresarial:** Exportadores (JSON/XML/PDF) sobre mismo árbol de dominio.
7. **Ventajas/desventajas:** agrega operaciones sin tocar modelo / costo de mantenimiento al agregar nuevos nodos.
8. **Variaciones/alternativas:** Pattern matching, estrategias por tipo.

---

## 6. Comparativas y decisiones de diseño

### 6.1 Strategy vs State

| Criterio | Strategy | State |
|---|---|---|
| Cambio de comportamiento | Por política externa | Por estado interno |
| Caso típico | métodos de pago | ciclo de vida pedido |

### 6.2 Decorator vs Proxy

| Criterio | Decorator | Proxy |
|---|---|---|
| Objetivo principal | Extender funcionalidad | Controlar acceso |
| Transparencia | Alta | Alta |

### 6.3 Factory vs Builder

| Criterio | Factory | Builder |
|---|---|---|
| Foco | qué tipo crear | cómo construir |
| Complejidad de objeto | baja-media | media-alta |

---

## 7. Conclusiones y recomendaciones

1. Selecciona patrón por **problema real**, no por catálogo.
2. Prioriza simplicidad antes de sobrearquitectura.
3. Combina patrones con SOLID para diseño sostenible.
4. Documenta decisiones: contexto, alternativas y trade-offs.
5. Refactoriza gradualmente cuando surjan señales de deuda técnica.

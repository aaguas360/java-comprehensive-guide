# EJEMPLOS PRÁCTICOS Y CASOS REALES EN JAVA

## Índice (Tabla de contenidos)
1. [Cómo usar este documento](#1-cómo-usar-este-documento)
2. [Encapsulamiento](#2-encapsulamiento)
3. [Herencia](#3-herencia)
4. [Polimorfismo](#4-polimorfismo)
5. [Abstracción](#5-abstracción)
6. [Interfaces](#6-interfaces)
7. [Clases abstractas](#7-clases-abstractas)
8. [Lambdas y Streams](#8-lambdas-y-streams)
9. [Optional](#9-optional)
10. [List, Map, Set y HashMap](#10-list-map-set-y-hashmap)
11. [Exceptions](#11-exceptions)
12. [SOLID aplicado](#12-solid-aplicado)
13. [Patrones de diseño en casos reales](#13-patrones-de-diseño-en-casos-reales)
14. [Generics](#14-generics)
15. [Concurrency](#15-concurrency)
16. [Conclusiones](#16-conclusiones)

---

## 1. Cómo usar este documento
Cada sección mantiene la estructura obligatoria:
- Definición técnica
- Definición sencilla
- Problema que resuelve
- Ejemplo Java completo
- Explicación técnica línea por línea
- Resultado esperado
- Caso real empresarial
- Buenas prácticas
- Errores comunes

---

## 2. Encapsulamiento
**Definición técnica:** Restricción de acceso al estado interno mediante modificadores y métodos.

**Definición sencilla:** Proteger datos para que no se cambien de forma incorrecta.

**Problema que resuelve:** Evita estados inválidos.

**Ejemplo Java completo:**
```java
public class CuentaBancaria {
    private double saldo;

    public CuentaBancaria(double saldoInicial) {
        if (saldoInicial < 0) throw new IllegalArgumentException("Saldo inválido");
        this.saldo = saldoInicial;
    }

    public void depositar(double monto) {
        if (monto <= 0) throw new IllegalArgumentException("Monto inválido");
        saldo += monto;
    }

    public double getSaldo() {
        return saldo;
    }

    public static void main(String[] args) {
        CuentaBancaria cuenta = new CuentaBancaria(100);
        cuenta.depositar(50);
        System.out.println(cuenta.getSaldo());
    }
}
```

**Explicación técnica línea por línea:**
- `private double saldo`: ocultamiento del atributo.
- Constructor valida estado inicial.
- `depositar` controla reglas de negocio.
- `getSaldo` expone solo lectura.
- `main` prueba el flujo.

**Resultado esperado:** `150.0`

**Caso real empresarial:** Core bancario, wallets, billeteras de puntos.

**Buenas prácticas:** Validar en constructor y métodos mutadores.

**Errores comunes:** Exponer setters públicos sin validación.

---

## 3. Herencia
**Definición técnica:** Mecanismo para derivar una clase de otra y reutilizar comportamiento.

**Definición sencilla:** Una clase “hija” hereda capacidades de una “madre”.

**Problema que resuelve:** Evita duplicación de lógica común.

**Ejemplo Java completo:**
```java
class Empleado {
    protected String nombre;

    public Empleado(String nombre) {
        this.nombre = nombre;
    }

    public String descripcion() {
        return "Empleado: " + nombre;
    }
}

class Desarrollador extends Empleado {
    public Desarrollador(String nombre) {
        super(nombre);
    }

    @Override
    public String descripcion() {
        return "Desarrollador: " + nombre;
    }
}

public class HerenciaDemo {
    public static void main(String[] args) {
        Empleado e = new Desarrollador("Laura");
        System.out.println(e.descripcion());
    }
}
```

**Explicación técnica línea por línea:**
- `Empleado`: clase base.
- `Desarrollador extends Empleado`: reutiliza y especializa.
- `@Override`: redefine comportamiento.
- Referencia de tipo base apunta al subtipo.

**Resultado esperado:** `Desarrollador: Laura`

**Caso real empresarial:** Modelos de usuarios: `Usuario`, `Administrador`, `Cliente`.

**Buenas prácticas:** Heredar solo con relación “es-un”.

**Errores comunes:** Herencia por conveniencia cuando era mejor composición.

---

## 4. Polimorfismo
**Definición técnica:** Capacidad de invocar distintas implementaciones a través de una misma abstracción.

**Definición sencilla:** Mismo botón, comportamientos distintos según objeto.

**Problema que resuelve:** Reduce condicionales por tipo.

**Ejemplo Java completo:**
```java
interface Pago {
    void procesar(double monto);
}

class PagoTarjeta implements Pago {
    public void procesar(double monto) {
        System.out.println("Pago tarjeta: " + monto);
    }
}

class PagoTransferencia implements Pago {
    public void procesar(double monto) {
        System.out.println("Pago transferencia: " + monto);
    }
}

public class PolimorfismoDemo {
    static void ejecutarPago(Pago pago, double monto) {
        pago.procesar(monto);
    }

    public static void main(String[] args) {
        ejecutarPago(new PagoTarjeta(), 200);
        ejecutarPago(new PagoTransferencia(), 200);
    }
}
```

**Explicación técnica línea por línea:** contrato `Pago`, implementaciones concretas y método consumidor desacoplado.

**Resultado esperado:**
- `Pago tarjeta: 200.0`
- `Pago transferencia: 200.0`

**Caso real empresarial:** Pasarelas de pago multi-proveedor.

**Buenas prácticas:** Programar contra interfaces.

**Errores comunes:** `if-else` por tipo en lugar de polimorfismo.

---

## 5. Abstracción
**Definición técnica:** Modelado de lo esencial ocultando detalles.

**Definición sencilla:** Mostrar “qué hace” sin exponer “cómo”.

**Problema que resuelve:** Reduce complejidad accidental.

**Ejemplo Java completo:**
```java
abstract class Reporte {
    public final void generar() {
        obtenerDatos();
        procesar();
        exportar();
    }

    protected abstract void obtenerDatos();
    protected abstract void procesar();

    private void exportar() {
        System.out.println("Exportado");
    }
}

class ReporteVentas extends Reporte {
    protected void obtenerDatos() { System.out.println("Datos ventas"); }
    protected void procesar() { System.out.println("Procesando ventas"); }
}

public class AbstraccionDemo {
    public static void main(String[] args) {
        new ReporteVentas().generar();
    }
}
```

**Explicación técnica línea por línea:** clase abstracta define flujo; subclase implementa pasos variables.

**Resultado esperado:**
- `Datos ventas`
- `Procesando ventas`
- `Exportado`

**Caso real empresarial:** Generación de reportes por área.

**Buenas prácticas:** Mantener estable el contrato abstracto.

**Errores comunes:** Mezclar detalles concretos dentro de la abstracción.

---

## 6. Interfaces
**Definición técnica:** Contratos de comportamiento sin estado de instancia mutable.

**Definición sencilla:** Reglas que una clase debe cumplir.

**Problema que resuelve:** Intercambiabilidad de implementaciones.

**Ejemplo Java completo:**
```java
interface Notificador {
    void enviar(String mensaje);
}

class NotificadorEmail implements Notificador {
    public void enviar(String mensaje) {
        System.out.println("Email enviado: " + mensaje);
    }
}

public class InterfacesDemo {
    public static void main(String[] args) {
        Notificador notificador = new NotificadorEmail();
        notificador.enviar("Pedido confirmado");
    }
}
```

**Explicación técnica línea por línea:** interfaz define contrato; clase concreta implementa; consumo desacoplado.

**Resultado esperado:** `Email enviado: Pedido confirmado`

**Caso real empresarial:** Drivers, gateways, adaptadores externos.

**Buenas prácticas:** Interfaces pequeñas (ISP).

**Errores comunes:** “god interfaces” con demasiados métodos.

---

## 7. Clases abstractas
**Definición técnica:** Clases incompletas que combinan contrato y lógica compartida.

**Definición sencilla:** Plantilla base parcialmente implementada.

**Problema que resuelve:** Reutilizar lógica común sin instanciar base.

**Ejemplo Java completo:**
```java
abstract class ValidadorDocumento {
    public boolean validar(String documento) {
        return documento != null && regla(documento);
    }

    protected abstract boolean regla(String documento);
}

class ValidadorDNI extends ValidadorDocumento {
    protected boolean regla(String documento) {
        return documento.matches("\\d{8}");
    }
}

public class AbstractaDemo {
    public static void main(String[] args) {
        System.out.println(new ValidadorDNI().validar("12345678"));
    }
}
```

**Explicación técnica línea por línea:** algoritmo base en clase abstracta y regla específica en subclase.

**Resultado esperado:** `true`

**Caso real empresarial:** Validadores por país.

**Buenas prácticas:** Extraer variaciones a métodos abstractos.

**Errores comunes:** Usarla cuando una interfaz era suficiente.

---

## 8. Lambdas y Streams
**Definición técnica:** Expresiones funcionales y procesamiento declarativo de colecciones.

**Definición sencilla:** Filtrar/transformar datos con menos código.

**Problema que resuelve:** Iteraciones verbosas y mutación innecesaria.

**Ejemplo Java completo:**
```java
import java.util.List;

public class StreamsDemo {
    public static void main(String[] args) {
        List<Integer> montos = List.of(100, 250, 80, 400);

        double totalMayoresA100 = montos.stream()
                .filter(m -> m > 100)
                .mapToDouble(m -> m)
                .sum();

        System.out.println(totalMayoresA100);
    }
}
```

**Explicación técnica línea por línea:** stream, filtro, transformación numérica y reducción.

**Resultado esperado:** `650.0`

**Caso real empresarial:** ETL liviano, analítica operacional.

**Buenas prácticas:** Streams sin efectos secundarios.

**Errores comunes:** Encadenamientos largos sin nombres intermedios.

---

## 9. Optional
**Definición técnica:** Contenedor para representar presencia/ausencia de valor sin `null` directo.

**Definición sencilla:** Caja que puede venir vacía.

**Problema que resuelve:** `NullPointerException` frecuentes.

**Ejemplo Java completo:**
```java
import java.util.Optional;

public class OptionalDemo {
    static Optional<String> buscarAlias(boolean existe) {
        return existe ? Optional.of("arquitecto-java") : Optional.empty();
    }

    public static void main(String[] args) {
        String alias = buscarAlias(false)
                .filter(a -> a.length() > 3)
                .orElse("invitado");
        System.out.println(alias);
    }
}
```

**Explicación técnica línea por línea:** función retorna `Optional`, filtra condición y fallback con `orElse`.

**Resultado esperado:** `invitado`

**Caso real empresarial:** Perfil parcial de cliente.

**Buenas prácticas:** Usar en retornos, no en campos de entidad.

**Errores comunes:** Llamar `get()` sin validar presencia.

---

## 10. List, Map, Set y HashMap
**Definición técnica:** Estructuras para almacenar elementos según necesidades de orden, unicidad y acceso por clave.

**Definición sencilla:** Distintas cajas para guardar datos.

**Problema que resuelve:** Persistencia temporal eficiente en memoria.

**Ejemplo Java completo:**
```java
import java.util.*;

public class ColeccionesPracticasDemo {
    public static void main(String[] args) {
        List<String> pedidos = new ArrayList<>(List.of("P1", "P2", "P2"));
        Set<String> pedidosUnicos = new HashSet<>(pedidos);
        Map<String, String> estadoPorPedido = new HashMap<>();
        estadoPorPedido.put("P1", "ENVIADO");
        estadoPorPedido.put("P2", "PENDIENTE");

        System.out.println(pedidos.size());
        System.out.println(pedidosUnicos.size());
        System.out.println(estadoPorPedido.get("P1"));
    }
}
```

**Explicación técnica línea por línea:** `List` admite repetidos, `Set` elimina duplicados, `Map` indexa por clave.

**Resultado esperado:**
- `3`
- `2`
- `ENVIADO`

**Caso real empresarial:** Gestión de pedidos y estados.

**Buenas prácticas:** Elegir estructura por patrón de acceso.

**Errores comunes:** Esperar orden en `HashMap`.

---

## 11. Exceptions
**Definición técnica:** Objetos que representan errores en runtime.

**Definición sencilla:** Señales de que algo salió mal.

**Problema que resuelve:** Manejo controlado de fallos.

**Ejemplo Java completo:**
```java
class ReglaNegocioException extends Exception {
    ReglaNegocioException(String message) { super(message); }
}

public class ExceptionsPracticoDemo {
    static void validarEdad(int edad) throws ReglaNegocioException {
        if (edad < 18) throw new ReglaNegocioException("Debe ser mayor de edad");
    }

    public static void main(String[] args) {
        try {
            validarEdad(16);
            System.out.println("Validación OK");
        } catch (ReglaNegocioException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Explicación técnica línea por línea:** excepción custom, propagación con `throws`, captura en `try-catch`.

**Resultado esperado:** `Error: Debe ser mayor de edad`

**Caso real empresarial:** Validaciones regulatorias.

**Buenas prácticas:** Excepciones semánticas por dominio.

**Errores comunes:** Ocultar errores con catches vacíos.

---

## 12. SOLID aplicado

### Tabla rápida

| Principio | Problema que evita |
|---|---|
| S | Clases “todopoderosas” |
| O | Cambios riesgosos por cada nueva regla |
| L | Subtipos incompatibles |
| I | Interfaces infladas |
| D | Acoplamiento rígido a implementaciones |

**Definición técnica:** Conjunto de principios para diseño orientado a mantenibilidad.

**Definición sencilla:** Reglas para que el código crezca sin romperse.

**Problema que resuelve:** Deuda técnica por acoplamiento y baja cohesión.

**Ejemplo Java completo:**
```java
interface Impuesto {
    double calcular(double base);
}

class ImpuestoGeneral implements Impuesto {
    public double calcular(double base) { return base * 0.21; }
}

class FacturaService {
    private final Impuesto impuesto;

    FacturaService(Impuesto impuesto) {
        this.impuesto = impuesto;
    }

    double total(double neto) {
        return neto + impuesto.calcular(neto);
    }
}

public class SolidPracticoDemo {
    public static void main(String[] args) {
        FacturaService service = new FacturaService(new ImpuestoGeneral());
        System.out.println(service.total(100));
    }
}
```

**Explicación técnica línea por línea:** dependencia por abstracción y extensión por nuevas implementaciones.

**Resultado esperado:** `121.0`

**Caso real empresarial:** Facturación multi-país.

**Buenas prácticas:** Inyección de dependencias.

**Errores comunes:** romper OCP con condicionales por tipo.

---

## 13. Patrones de diseño en casos reales
**Definición técnica:** Soluciones reutilizables a problemas recurrentes de diseño.

**Definición sencilla:** Recetas probadas para arquitecturas comunes.

**Problema que resuelve:** Reinventar soluciones y propagar antipatrones.

**Ejemplo Java completo (Strategy):**
```java
interface EnvioStrategy { double costo(double peso); }
class EnvioEstandar implements EnvioStrategy { public double costo(double peso) { return 5 + peso; } }
class EnvioExpress implements EnvioStrategy { public double costo(double peso) { return 15 + (2 * peso); } }

class CotizadorEnvio {
    private final EnvioStrategy strategy;
    CotizadorEnvio(EnvioStrategy strategy) { this.strategy = strategy; }
    double cotizar(double peso) { return strategy.costo(peso); }
}

public class PatronesDemo {
    public static void main(String[] args) {
        System.out.println(new CotizadorEnvio(new EnvioExpress()).cotizar(3));
    }
}
```

**Explicación técnica línea por línea:** encapsulación de algoritmo variable vía estrategia.

**Resultado esperado:** `21.0`

**Caso real empresarial:** Selección dinámica de proveedor logístico.

**Buenas prácticas:** Documentar cuándo aplicar cada patrón.

**Errores comunes:** Aplicar patrones sin problema real.

---

## 14. Generics
**Definición técnica:** Parametrización de tipos para seguridad en compilación.

**Definición sencilla:** Reutilizar código para distintos tipos sin perder control.

**Problema que resuelve:** Castings inseguros.

**Ejemplo Java completo:**
```java
class Repositorio<T> {
    private T valor;
    void guardar(T valor) { this.valor = valor; }
    T obtener() { return valor; }
}

public class GenericsDemo {
    public static void main(String[] args) {
        Repositorio<String> repo = new Repositorio<>();
        repo.guardar("ok");
        System.out.println(repo.obtener().toUpperCase());
    }
}
```

**Explicación técnica línea por línea:** tipo genérico `T` evita casting y errores de tipo.

**Resultado esperado:** `OK`

**Caso real empresarial:** Repositorios, colas, caches genéricas.

**Buenas prácticas:** Nombres de tipo semánticos (`T`, `K`, `V`, `E`).

**Errores comunes:** usar tipos raw (`List` sin `<Tipo>`).

---

## 15. Concurrency
**Definición técnica:** Ejecución concurrente para mejorar throughput y latencia.

**Definición sencilla:** Hacer varias tareas “al mismo tiempo”.

**Problema que resuelve:** Bloqueo de procesos secuenciales lentos.

**Ejemplo Java completo:**
```java
import java.util.concurrent.CompletableFuture;

public class ConcurrencyDemo {
    public static void main(String[] args) {
        CompletableFuture<String> usuario = CompletableFuture.supplyAsync(() -> "usuario-ok");
        CompletableFuture<String> score = CompletableFuture.supplyAsync(() -> "score-720");

        String resultado = usuario.thenCombine(score, (u, s) -> u + "|" + s).join();
        System.out.println(resultado);
    }
}
```

**Explicación técnica línea por línea:** dos tareas asíncronas, combinación no bloqueante y sincronización final.

**Resultado esperado:** `usuario-ok|score-720`

**Caso real empresarial:** Orquestación de servicios en evaluación crediticia.

**Buenas prácticas:** Timeouts, pools dedicados, manejo de excepciones.

**Errores comunes:** Bloquear con `get()` temprano y perder paralelismo.

---

## 16. Conclusiones
1. Aprender Java requiere pasar de sintaxis a diseño.
2. Los ejemplos deben conectarse con problemas reales de negocio.
3. SOLID + colecciones + concurrencia bien aplicada = software mantenible.
4. Prioriza claridad, testabilidad y observabilidad desde el inicio.


# GUÍA COMPLETA DE CONCEPTOS FUNDAMENTALES DE PROGRAMACIÓN EN JAVA

## Índice (Tabla de contenidos)
1. [Introducción y ruta de aprendizaje](#1-introducción-y-ruta-de-aprendizaje)
2. [Fundamentos de programación](#2-fundamentos-de-programación)
3. [Estructuras de control](#3-estructuras-de-control)
4. [Ciclos](#4-ciclos)
5. [Métodos](#5-métodos)
6. [Programación Orientada a Objetos (POO)](#6-programación-orientada-a-objetos-poo)
7. [Programación funcional en Java](#7-programación-funcional-en-java)
8. [Colecciones Java](#8-colecciones-java)
9. [Manipulación de Strings](#9-manipulación-de-strings)
10. [Convenciones Java y Clean Code](#10-convenciones-java-y-clean-code)
11. [Manejo de errores](#11-manejo-de-errores)
12. [Principios SOLID](#12-principios-solid)
13. [Conceptos avanzados](#13-conceptos-avanzados)
14. [Tablas comparativas rápidas](#14-tablas-comparativas-rápidas)
15. [Conclusiones y buenas prácticas globales](#15-conclusiones-y-buenas-prácticas-globales)

---

## 1. Introducción y ruta de aprendizaje

Esta guía está diseñada para **Junior, Semi Senior y Senior** con progresión desde fundamentos hasta concurrencia.

Diagrama conceptual:

```text
Fundamentos -> Control de flujo -> Métodos -> POO -> Funcional -> Colecciones
      -> Manejo de errores -> SOLID -> Concurrencia -> Diseño de software robusto
```

---

## 2. Fundamentos de programación

### 2.1 Qué es programar
1. **Definición técnica:** Diseñar instrucciones formales para que una máquina ejecute una tarea.
2. **Definición no técnica:** Escribir una receta exacta para que la computadora haga algo útil.
3. **Caso real:** Automatizar cálculo de nómina.
4. **Ventajas:** Automatización, escalabilidad, repetibilidad.
5. **Desventajas/consideraciones:** Curva de aprendizaje, mantenimiento.
6. **Buenas prácticas:** Separar problema, lógica y validaciones.
7. **Errores comunes:** Codificar sin entender reglas de negocio.
8. **Ejemplo Java completo:**
```java
public class ProgramarEjemplo {
    public static void main(String[] args) {
        int horas = 40;
        double tarifa = 15.5;
        double pago = horas * tarifa;
        System.out.println("Pago semanal: " + pago);
    }
}
```
9. **Explicación línea por línea:**
- `class ProgramarEjemplo`: contenedor del programa.
- `main`: punto de entrada.
- `horas/tarifa`: entradas.
- `pago = horas * tarifa`: lógica.
- `println`: salida.
10. **Pregunta de entrevista:** ¿Qué diferencia hay entre programar y diseñar software?
11. **Respuesta esperada:** Programar implementa; diseñar define arquitectura, componentes y decisiones de largo plazo.

### 2.2 Algoritmos
1. **Definición técnica:** Secuencia finita y ordenada de pasos para resolver un problema.
2. **Definición no técnica:** Instrucciones paso a paso para llegar a un resultado.
3. **Caso real:** Seleccionar la ruta más corta de entregas.
4. **Ventajas:** Claridad, optimización.
5. **Desventajas:** Puede ser complejo optimizar.
6. **Buenas prácticas:** Medir complejidad temporal/espacial.
7. **Errores comunes:** Ignorar casos límite.
8. **Ejemplo Java completo:**
```java
public class MaximoEjemplo {
    public static int maximo(int[] nums) {
        int max = nums[0];
        for (int n : nums) {
            if (n > max) max = n;
        }
        return max;
    }

    public static void main(String[] args) {
        System.out.println(maximo(new int[]{3, 9, 2, 7}));
    }
}
```
9. **Explicación:** Inicializa máximo, recorre, compara, actualiza, retorna.
10. **Pregunta:** ¿Cómo evalúas un algoritmo?
11. **Respuesta:** Correctitud, complejidad Big-O y uso de memoria.

### 2.3 Pseudocódigo
1. **Definición técnica:** Descripción semiformal de algoritmo sin sintaxis estricta de lenguaje.
2. **Definición no técnica:** Borrador entendible antes de codificar.
3. **Caso real:** Definir validaciones de checkout antes de implementar.
4. **Ventajas:** Comunicación entre negocio y desarrollo.
5. **Desventajas:** No ejecutable.
6. **Buenas prácticas:** Usar entradas/salidas y decisiones explícitas.
7. **Errores comunes:** Ambigüedad en pasos.
8. **Ejemplo Java completo (tras pseudocódigo):**
```java
public class ParImpar {
    public static void main(String[] args) {
        int numero = 11;
        if (numero % 2 == 0) {
            System.out.println("Par");
        } else {
            System.out.println("Impar");
        }
    }
}
```
9. **Explicación:** `%` calcula residuo; `if` decide salida.
10. **Pregunta:** ¿Cuándo conviene pseudocódigo?
11. **Respuesta:** Al definir lógica compleja antes de implementación.

### 2.4 Variables
1. Definición técnica: Espacio nombrado de memoria cuyo valor puede cambiar.
2. Definición no técnica: Caja con etiqueta para guardar datos.
3. Caso real: Cantidad en carrito de compras.
4. Ventajas: Flexibilidad en cálculos.
5. Consideraciones: Scope y tipo correcto.
6. Buenas prácticas: Nombres descriptivos.
7. Errores comunes: Reutilizar variables para significados distintos.
8. Ejemplo Java:
```java
public class VariablesDemo {
    public static void main(String[] args) {
        int stock = 20;
        stock = stock - 3;
        System.out.println(stock);
    }
}
```
9. Explicación: declara, actualiza, imprime.
10. Pregunta: ¿Diferencia entre variable local e instancia?
11. Respuesta: Local vive en método; instancia vive con objeto.

### 2.5 Tipos de datos
1. Definición técnica: Clasificación de datos que define operaciones válidas y memoria.
2. Definición no técnica: Regla del tipo de contenido permitido en una caja.
3. Caso real: `String` para email, `double` para precio.
4. Ventajas: Seguridad de compilación.
5. Consideraciones: Conversiones y precisión.
6. Buenas prácticas: Elegir tipo mínimo suficiente.
7. Errores comunes: Usar `double` para dinero sin estrategia.
8. Ejemplo Java:
```java
public class TiposDatosDemo {
    public static void main(String[] args) {
        int edad = 30;
        double saldo = 99.95;
        boolean activo = true;
        String nombre = "Ana";
        System.out.println(nombre + " - " + edad + " - " + saldo + " - " + activo);
    }
}
```
9. Explicación: cada variable representa un tipo distinto.
10. Pregunta: ¿Primitivo vs referencia?
11. Respuesta: Primitivo almacena valor; referencia apunta a objeto.

### 2.6 Constantes
1. Definición técnica: Variable inmutable declarada con `final`.
2. Definición no técnica: Dato fijo que no debe cambiar.
3. Caso real: Tasa de IVA.
4. Ventajas: Evita cambios accidentales.
5. Consideraciones: No abusar de valores globales.
6. Buenas prácticas: `static final` y mayúsculas.
7. Errores comunes: Hardcodear literales repetidos.
8. Ejemplo Java:
```java
public class ConstantesDemo {
    private static final double IVA = 0.21;

    public static void main(String[] args) {
        double base = 100;
        System.out.println(base + (base * IVA));
    }
}
```
9. Explicación: `IVA` es constante de clase.
10. Pregunta: ¿Qué protege `final`?
11. Respuesta: Reasignación de referencia/variable.

### 2.7 Operadores

| Tipo | Uso | Ejemplo |
|---|---|---|
| Aritméticos | Cálculos | `+ - * / %` |
| Relacionales | Comparar | `== != > < >= <=` |
| Lógicos | Condiciones compuestas | `&& || !` |
| Asignación | Asignar/actualizar | `= += -= *=` |
| Ternario | Decisión compacta | `cond ? a : b` |

1. Definición técnica: Símbolos para transformar/relacionar operandos.
2. Definición no técnica: Acciones sobre datos (sumar, comparar, decidir).
3. Caso real: Reglas de descuento.
4. Ventajas: Expresividad.
5. Consideraciones: Prioridad de operadores.
6. Buenas prácticas: Paréntesis para claridad.
7. Errores comunes: Confundir `=` con `==`.
8. Ejemplo Java:
```java
public class OperadoresDemo {
    public static void main(String[] args) {
        int a = 10, b = 3;
        int suma = a + b;
        boolean mayor = a > b;
        boolean ambosPositivos = a > 0 && b > 0;
        a += 5;
        String tipo = (a % 2 == 0) ? "par" : "impar";
        System.out.println(suma + " " + mayor + " " + ambosPositivos + " " + tipo);
    }
}
```
9. Explicación: muestra operador por categoría.
10. Pregunta: ¿Cuándo evitar ternario?
11. Respuesta: Cuando la expresión pierde legibilidad.

---

## 3. Estructuras de control

### 3.1 if, if-else, if-else if, switch, switch expression, ternario
1. Definición técnica: Mecanismos de selección de flujo.
2. Definición no técnica: Caminos alternativos según condición.
3. Caso real: Clasificar riesgo crediticio.
4. Ventajas: Control explícito de reglas.
5. Consideraciones: Complejidad ciclomática alta.
6. Buenas prácticas: Preferir claridad y extraer métodos.
7. Errores comunes: Cascadas largas sin refactor.
8. Ejemplo Java completo:
```java
public class ControlFlujoDemo {
    public static void main(String[] args) {
        int score = 78;

        if (score >= 90) {
            System.out.println("A");
        } else if (score >= 70) {
            System.out.println("B");
        } else {
            System.out.println("C");
        }

        String canal = "WEB";
        switch (canal) {
            case "APP":
                System.out.println("Canal móvil");
                break;
            case "WEB":
                System.out.println("Canal web");
                break;
            default:
                System.out.println("Canal otro");
        }

        String nivel = switch (score / 10) {
            case 10, 9 -> "EXCELENTE";
            case 8, 7 -> "BUENO";
            default -> "MEJORABLE";
        };

        String estado = score >= 60 ? "Aprobado" : "Reprobado";
        System.out.println(nivel + " - " + estado);
    }
}
```
9. Explicación línea por línea: bloque condicional clásico, `switch` tradicional con `break`, `switch expression` que retorna valor, ternario para decisión corta.
10. Pregunta: ¿Cuándo usar `switch expression`?
11. Respuesta: Cuando se desea mapear entradas a valores de forma más segura y concisa.

---

## 4. Ciclos

### 4.1 for, foreach, while, do while, break, continue
1. Definición técnica: Estructuras iterativas para repetición controlada.
2. Definición no técnica: Repetir tareas hasta cumplir una condición.
3. Caso real: Procesamiento de lotes.
4. Ventajas: Automatizan iteraciones.
5. Consideraciones: Riesgo de loops infinitos.
6. Buenas prácticas: Condiciones claras y límite seguro.
7. Errores comunes: Modificar colección durante foreach sin iterador.
8. Ejemplo Java:
```java
import java.util.List;

public class CiclosDemo {
    public static void main(String[] args) {
        for (int i = 0; i < 3; i++) {
            System.out.println("for: " + i);
        }

        for (String n : List.of("Ana", "Luis", "Marta")) {
            if (n.startsWith("L")) continue;
            System.out.println("foreach: " + n);
        }

        int x = 0;
        while (x < 5) {
            if (x == 3) break;
            System.out.println("while: " + x);
            x++;
        }

        int y = 0;
        do {
            System.out.println("do-while: " + y);
            y++;
        } while (y < 2);
    }
}
```
9. Explicación: cada tipo de ciclo y control de corte/salto.
10. Pregunta: ¿Diferencia clave `while` vs `do while`?
11. Respuesta: `do while` ejecuta al menos una vez.

---

## 5. Métodos

### 5.1 Definición, parámetros, retorno, sobrecarga, scope
1. Definición técnica: Bloque reutilizable que encapsula comportamiento.
2. Definición no técnica: Mini-función con trabajo específico.
3. Caso real: Calcular impuestos en distintos módulos.
4. Ventajas: Reutilización y testabilidad.
5. Consideraciones: Cohesión y tamaño.
6. Buenas prácticas: Una responsabilidad por método.
7. Errores comunes: Métodos gigantes con múltiples razones de cambio.
8. Ejemplo Java:
```java
public class MetodosDemo {
    public static void main(String[] args) {
        System.out.println(sumar(2, 3));
        System.out.println(sumar(2, 3, 4));
    }

    static int sumar(int a, int b) {
        int resultado = a + b; // variable local (scope local)
        return resultado;
    }

    static int sumar(int a, int b, int c) { // sobrecarga
        return a + b + c;
    }
}
```
9. Explicación: firma, parámetros, retorno y sobrecarga por distinta aridad.
10. Pregunta: ¿Qué define la sobrecarga válida?
11. Respuesta: Mismo nombre, distinta lista de parámetros.

---

## 6. Programación Orientada a Objetos (POO)

### 6.1 Conceptos base

| Concepto | Definición breve | Ejemplo |
|---|---|---|
| Clase | Molde de objetos | `class Cuenta {}` |
| Objeto | Instancia de clase | `new Cuenta()` |
| Atributo | Estado del objeto | `private double saldo;` |
| Método | Comportamiento | `depositar()` |

Cobertura explícita de conceptos POO en esta sección: **Encapsulamiento, Herencia, Polimorfismo, Abstracción, Interfaces, Clases abstractas, Asociación, Agregación y Composición**.

### 6.2 Encapsulamiento, herencia, polimorfismo, abstracción, interfaces, abstractas, asociación/agregación/composición
1. Definición técnica: Principios para modelar dominio y desacoplar implementación.
2. Definición no técnica: Organizar software como piezas con responsabilidades claras.
3. Caso real: Sistema bancario.
4. Ventajas: Mantenibilidad, extensión.
5. Consideraciones: Sobrediseño.
6. Buenas prácticas: Programar contra interfaces.
7. Errores comunes: Exponer atributos públicos.
8. Ejemplo Java completo:
```java
interface Notificador {
    void enviar(String mensaje);
}

abstract class Persona {
    protected String nombre;
    public Persona(String nombre) { this.nombre = nombre; }
    public abstract String rol();
}

class Cliente extends Persona {
    private double saldo;

    public Cliente(String nombre, double saldo) {
        super(nombre);
        this.saldo = saldo;
    }

    public void depositar(double monto) { // encapsulamiento
        if (monto > 0) saldo += monto;
    }

    @Override
    public String rol() { return "CLIENTE"; }

    public double getSaldo() { return saldo; }
}

class EmailNotificador implements Notificador {
    @Override
    public void enviar(String mensaje) {
        System.out.println("Email: " + mensaje);
    }
}

class BancoService { // asociación con Notificador
    private final Notificador notificador;

    public BancoService(Notificador notificador) {
        this.notificador = notificador;
    }

    public void acreditar(Cliente cliente, double monto) {
        cliente.depositar(monto); // composición de comportamiento
        notificador.enviar("Acreditación a " + cliente.nombre + ": " + monto);
    }
}

public class PooDemo {
    public static void main(String[] args) {
        Cliente c = new Cliente("Lucía", 100);
        BancoService service = new BancoService(new EmailNotificador());
        service.acreditar(c, 50);
        Persona p = c; // polimorfismo
        System.out.println(p.rol() + " saldo=" + c.getSaldo());
    }
}
```
9. Explicación línea por línea: interfaz para contrato, abstracta para comportamiento común, clase concreta encapsula estado, servicio usa dependencia por interfaz, polimorfismo en referencia `Persona`.
10. Pregunta: ¿Agregación vs composición?
11. Respuesta: En agregación, partes pueden vivir separadas; en composición, dependen del ciclo de vida del contenedor.

---

## 7. Programación funcional en Java

### 7.1 Lambda, Functional Interface, Predicate, Function, Consumer, Supplier, Method Reference, Streams, Optional
1. Definición técnica: Paradigma declarativo sobre funciones y transformaciones inmutables.
2. Definición no técnica: Decir *qué* quieres obtener más que *cómo* iterar paso a paso.
3. Caso real: Filtrado y agregación de órdenes.
4. Ventajas: Menos código boilerplate.
5. Consideraciones: Abuso puede dificultar depuración.
6. Buenas prácticas: Streams sin efectos secundarios.
7. Errores comunes: Usar `Optional` como atributo de entidad.
8. Ejemplo Java:
```java
import java.util.List;
import java.util.Optional;
import java.util.function.*;

public class FuncionalDemo {
    public static void main(String[] args) {
        Predicate<Integer> esPar = n -> n % 2 == 0;
        Function<Integer, Integer> cuadrado = n -> n * n;
        Consumer<Integer> imprimir = System.out::println;
        Supplier<String> origen = () -> "sistema";

        List<Integer> datos = List.of(1, 2, 3, 4, 5);
        datos.stream()
             .filter(esPar)
             .map(cuadrado)
             .forEach(imprimir);

        Optional<String> nombre = Optional.ofNullable(null);
        String valor = nombre.orElseGet(() -> "anónimo-" + origen.get());
        System.out.println(valor);
    }
}
```
9. Explicación: interfaces funcionales, referencia de método, pipeline stream y manejo seguro de null con Optional.
10. Pregunta: ¿`map` vs `flatMap`?
11. Respuesta: `map` transforma 1 a 1; `flatMap` aplana estructuras anidadas.

---

## 8. Colecciones Java

### 8.1 Resumen comparativo

| Estructura | Orden | Duplicados | Complejidad típica búsqueda |
|---|---|---|---|
| ArrayList | Inserción ordenada | Sí | O(n) |
| LinkedList | Inserción ordenada | Sí | O(n) |
| HashSet | No garantizado | No | O(1) promedio |
| TreeSet | Ordenado | No | O(log n) |
| HashMap | No garantizado | Claves únicas | O(1) promedio |
| TreeMap | Ordenado por clave | Claves únicas | O(log n) |
| LinkedHashMap | Inserción/acceso | Claves únicas | O(1) promedio |
| Queue | FIFO | Sí | O(1) extremo |
| Stack | LIFO | Sí | O(1) extremo |

### 8.2 Ficha unificada (List, Set, Map, Queue, Stack y variantes)
1. Definición técnica: APIs para estructuras de datos genéricas.
2. Definición no técnica: Distintas formas de guardar y recuperar datos.
3. Caso real: Catálogo, sesión de usuario, colas de procesamiento.
4. Ventajas: Implementaciones optimizadas.
5. Consideraciones: Elegir estructura por patrón de acceso.
6. Buenas prácticas: Programar con interfaz (`List`, `Map`).
7. Errores comunes: Asumir orden en `HashMap`/`HashSet`.
8. Ejemplo Java:
```java
import java.util.*;

public class ColeccionesDemo {
    public static void main(String[] args) {
        List<String> lista = new ArrayList<>();
        lista.add("A");
        lista.add("B");

        Set<String> set = new TreeSet<>(lista);

        Map<String, Integer> mapa = new LinkedHashMap<>();
        mapa.put("A", 1);
        mapa.put("B", 2);

        Queue<String> cola = new LinkedList<>();
        cola.offer("tarea-1");

        Stack<String> stack = new Stack<>();
        stack.push("operacion-1");

        System.out.println(lista + " | " + set + " | " + mapa + " | " + cola.poll() + " | " + stack.pop());
    }
}
```
9. Explicación: se construyen y usan colecciones por su semántica.
10. Pregunta: ¿Cuándo `ArrayList` vs `LinkedList`?
11. Respuesta: `ArrayList` para lecturas por índice; `LinkedList` para inserciones/borrados frecuentes en extremos.

---

## 9. Manipulación de Strings

### 9.1 Métodos clave

| Método | Propósito | Nota |
|---|---|---|
| `equals` / `equalsIgnoreCase` | Comparar contenido | Evitar `==` |
| `compareTo` / `compareToIgnoreCase` | Orden lexicográfico | 0 si iguales |
| `contains` | Subcadena | Sensible a mayúsculas |
| `startsWith` / `endsWith` | Prefijo/sufijo | Validaciones rápidas |
| `matches` | Validación por regex | Útil para formato |
| `substring` | Extraer por índice | Cuidado con límites |
| `split` | Separar por regex | `"\\,"` en comas literales no necesario |
| `replace` | Sustitución | No muta original |
| `trim` | Quita bordes en blanco | No quita internos |
| `isEmpty` / `isBlank` | Vacío/blancos | `isBlank` desde Java 11 |

1. Definición técnica: API inmutable de `String` para comparación y transformación.
2. Definición no técnica: Herramientas para limpiar y validar texto.
3. Caso real: Validar datos de formulario.
4. Ventajas: API extensa e inmutable.
5. Consideraciones: `split` usa regex.
6. Buenas prácticas: Validar `null` antes.
7. Errores comunes: Esperar que `replace` cambie original.
8. Ejemplo Java:
```java
public class StringsDemo {
    public static void main(String[] args) {
        String correo = "  Usuario@Empresa.com  ";
        String limpio = correo.trim();

        System.out.println(limpio.equalsIgnoreCase("usuario@empresa.com"));
        System.out.println(limpio.compareToIgnoreCase("USUARIO@EMPRESA.COM"));
        System.out.println(limpio.contains("@"));
        System.out.println(limpio.startsWith("Usuario"));
        System.out.println(limpio.endsWith(".com"));
        System.out.println(limpio.matches("^[A-Za-z]+@Empresa\\.com$"));
        System.out.println(limpio.substring(0, 7));
        System.out.println(String.join("|", limpio.split("@")));
        System.out.println(limpio.replace("Empresa", "Negocio"));
        System.out.println("".isEmpty());
        System.out.println("   ".isBlank());
    }
}
```
9. Explicación: limpieza, comparación, búsquedas y transformaciones inmutables.
10. Pregunta: ¿`isEmpty` vs `isBlank`?
11. Respuesta: `isEmpty` longitud 0; `isBlank` solo espacios también cuenta como vacío lógico.

---

## 10. Convenciones Java y Clean Code

### 10.1 Convenciones
- **Camel Case:** variables y métodos (`totalAmount`, `calculateTax`).
- **Pascal Case:** clases (`InvoiceService`).
- **Snake Case:** solo en constantes o contextos externos (`MAX_RETRIES`).
- **Naming conventions:** nombres que expresen intención.
- **Clean Code:** funciones pequeñas, bajo acoplamiento, alta cohesión.

1. Definición técnica: Estándares para consistencia semántica y mantenibilidad.
2. Definición no técnica: Formas comunes de nombrar para que todos entiendan.
3. Caso real: Equipos grandes con múltiples contributors.
4. Ventajas: Menor deuda técnica.
5. Consideraciones: Requiere disciplina de equipo.
6. Buenas prácticas: Revisiones de código con checklist.
7. Errores comunes: Abreviaturas crípticas.
8. Ejemplo Java:
```java
public class InvoiceService {
    private static final int MAX_RETRIES = 3;

    public double calculateTotalAmount(double netAmount, double taxRate) {
        return netAmount + (netAmount * taxRate);
    }
}
```
9. Explicación: clase en PascalCase, método en camelCase, constante en upper snake.
10. Pregunta: ¿Qué hace “clean” un método?
11. Respuesta: Nombre claro, responsabilidad única, pocos parámetros y sin efectos sorpresa.

---

## 11. Manejo de errores

### 11.1 Exception, RuntimeException, Checked/Unchecked, try-catch-finally, throw, throws, custom

Términos clave de esta sección: **Try-Catch-Finally**, **Checked Exception**, **Unchecked Exception** y **Excepciones personalizadas**.
1. Definición técnica: Modelo de control para condiciones excepcionales en ejecución.
2. Definición no técnica: Forma controlada de tratar errores sin tumbar todo el sistema.
3. Caso real: Fallo en pasarela de pago.
4. Ventajas: Propagación explícita y recuperación.
5. Consideraciones: No usar excepciones para flujo normal.
6. Buenas prácticas: Mensajes útiles y wrapping contextual.
7. Errores comunes: `catch (Exception)` indiscriminado.
8. Ejemplo Java:
```java
class SaldoInsuficienteException extends Exception {
    public SaldoInsuficienteException(String message) { super(message); }
}

public class ExcepcionesDemo {
    static void retirar(double saldo, double monto) throws SaldoInsuficienteException {
        if (monto > saldo) {
            throw new SaldoInsuficienteException("Saldo insuficiente. saldo=" + saldo + ", monto=" + monto);
        }
    }

    public static void main(String[] args) {
        try {
            retirar(100, 150);
        } catch (SaldoInsuficienteException e) {
            System.out.println("Error de negocio: " + e.getMessage());
        } catch (RuntimeException e) {
            System.out.println("Error no controlado: " + e.getMessage());
        } finally {
            System.out.println("Auditoría finalizada");
        }
    }
}
```
9. Explicación: excepción checked personalizada, propagación con `throws`, disparo con `throw`, manejo en `try-catch-finally`.
10. Pregunta: ¿Cuándo checked vs unchecked?
11. Respuesta: Checked para errores recuperables/esperados; unchecked para fallos de programación o irreversibles.

---

## 12. Principios SOLID

### 12.1 S — Single Responsibility Principle
- **Técnico:** una clase debe tener una sola razón de cambio.
- **Sencillo:** una clase debe hacer una sola cosa bien.
- **Caso real:** separar `InvoiceCalculator` de `InvoicePrinter`.
- **Ventajas:** pruebas simples.
- **Riesgo:** exceso de clases pequeñas sin criterio.

### 12.2 O — Open/Closed Principle
- Abierto a extensión, cerrado a modificación.
- Caso real: nuevas estrategias de descuento sin tocar clase base.

### 12.3 L — Liskov Substitution Principle
- Subtipos deben sustituir al tipo base sin romper contratos.
- Caso real: implementaciones de `PaymentMethod` intercambiables.

### 12.4 I — Interface Segregation Principle
- Interfaces pequeñas y específicas.
- Caso real: `ReadableRepository` y `WritableRepository`.

### 12.5 D — Dependency Inversion Principle
- Depender de abstracciones, no concreciones.
- Caso real: inyección de `NotificationGateway`.

Ejemplo Java completo (aplicando SOLID):
```java
interface DiscountPolicy {
    double apply(double amount);
}

class NoDiscount implements DiscountPolicy {
    public double apply(double amount) { return amount; }
}

class VipDiscount implements DiscountPolicy {
    public double apply(double amount) { return amount * 0.9; }
}

class InvoiceCalculator {
    private final DiscountPolicy discountPolicy;

    public InvoiceCalculator(DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }

    public double total(double subtotal) {
        return discountPolicy.apply(subtotal);
    }
}

public class SolidDemo {
    public static void main(String[] args) {
        InvoiceCalculator calculator = new InvoiceCalculator(new VipDiscount());
        System.out.println(calculator.total(100));
    }
}
```
Pregunta típica: ¿Cómo se relaciona OCP con Strategy?
Respuesta esperada: Strategy permite extender comportamientos (nuevas estrategias) sin modificar el consumidor.

---

## 13. Conceptos avanzados

### 13.1 Generics, Enum, Record, Annotations, Reflection, Thread, Concurrency, CompletableFuture
1. Definición técnica: Herramientas de tipado, metadatos, metaprogramación y concurrencia.
2. Definición no técnica: Funciones avanzadas para software robusto y moderno.
3. Caso real: APIs genéricas y procesamiento asíncrono.
4. Ventajas: Seguridad de tipos y mejor uso de recursos.
5. Consideraciones: complejidad técnica.
6. Buenas prácticas: evitar reflection salvo necesidad; usar `ExecutorService`.
7. Errores comunes: crear hilos sin control.
8. Ejemplo Java:
```java
import java.lang.annotation.*;
import java.util.concurrent.*;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@interface Entidad {}

@Entidad
record Usuario(String id, String nombre) {}

enum Prioridad { BAJA, MEDIA, ALTA }

class Caja<T> {
    private T valor;
    public Caja(T valor) { this.valor = valor; }
    public T getValor() { return valor; }
}

public class AvanzadoDemo {
    public static void main(String[] args) throws Exception {
        Caja<Usuario> caja = new Caja<>(new Usuario("u1", "Ana"));
        System.out.println(caja.getValor());

        boolean anotada = caja.getValor().getClass().isAnnotationPresent(Entidad.class);
        System.out.println("Anotada: " + anotada + " prioridad=" + Prioridad.ALTA);

        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> "OK");
        System.out.println(future.thenApply(v -> v + "-ASYNC").get());
    }
}
```
9. Explicación: generic tipado, `record` inmutable, `enum` controlado, annotation+reflection para metadatos, concurrencia con `CompletableFuture`.
10. Pregunta: ¿Ventaja principal de `CompletableFuture`?
11. Respuesta: Componer tareas asíncronas no bloqueantes con manejo de errores encadenado.

---

## 14. Tablas comparativas rápidas

### 14.1 Checked vs Unchecked

| Tipo | Verificación | Ejemplo | Uso |
|---|---|---|---|
| Checked | Compilación | `IOException` | Errores recuperables |
| Unchecked | Runtime | `NullPointerException` | Errores de programación |

### 14.2 Herencia vs Composición

| Enfoque | Ventaja | Riesgo |
|---|---|---|
| Herencia | Reuso directo | Acoplamiento rígido |
| Composición | Flexibilidad | Más objetos/configuración |

### 14.3 while vs for

| Criterio | while | for |
|---|---|---|
| Iteraciones conocidas | Menos explícito | Ideal |
| Iteraciones condicionales | Ideal | Posible pero menos claro |

---

## 15. Conclusiones y buenas prácticas globales

1. Prioriza **legibilidad** por encima de “código ingenioso”.
2. Diseña primero contratos (`interface`) y luego implementaciones.
3. Usa colecciones y concurrencia según necesidad real, no por moda.
4. Maneja errores con contexto de negocio y logs útiles.
5. Aplica SOLID gradualmente y mide impacto en mantenibilidad.
6. Refactoriza de forma incremental con pruebas.

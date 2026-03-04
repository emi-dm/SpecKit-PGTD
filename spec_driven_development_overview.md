<table bgcolor="#ffffff" width="100%" style="width: 100%; border-collapse: collapse; border: 1px solid #d0d0d0; background-color: #ffffff !important; font-family: Arial, sans-serif; opacity: 1 !important;">
  <tr bgcolor="#ffffff" style="background-color: #ffffff !important;">
    <td align="center" bgcolor="#ffffff" style="padding: 25px; vertical-align: middle; background-color: #ffffff !important;">
      <div style="background-color: #ffffff !important; padding: 10px;">
        <img src="https://talentodigitalextremadura.com/wp-content/uploads/2025/05/junta-ext-transforma2.png" height="140" style="height: 140px; width: auto; display: inline-block; background-color: #ffffff !important;">
      </div>
      <hr style="border: 0; border-top: 1px solid #dddddd; width: 85%; margin: 20px auto;">
      <table width="100%" bgcolor="#ffffff" style="width: 100%; border-collapse: collapse; background-color: #ffffff !important;">
        <tr bgcolor="#ffffff" style="background-color: #ffffff !important;">
          <td align="center" width="33.3%" bgcolor="#ffffff" style="padding: 10px; background-color: #ffffff !important; border: none;">
            <img src="https://talentodigitalextremadura.com/wp-content/uploads/2024/10/Grafismo-UEx-Color-3.png" height="110" style="height: 110px; width: auto; background-color: #ffffff !important;">
          </td>
          <td align="center" width="33.3%" bgcolor="#ffffff" style="padding: 10px; background-color: #ffffff !important; border: none;">
            <img src="https://talentodigitalextremadura.com/wp-content/uploads/2026/01/logointia.png" height="110" style="height: 110px; width: auto; background-color: #ffffff !important;">
          </td>
          <td align="center" width="33.3%" bgcolor="#ffffff" style="padding: 10px; background-color: #ffffff !important; border: none;">
            <img src="https://talentodigitalextremadura.com/wp-content/uploads/2024/10/Group-59651.png" height="110" style="height: 110px; width: auto; background-color: #ffffff !important;">
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table>

# Spec-Driven Development (SDD): De Código a Contrato

## 1. Introducción

Durante décadas, el código ha sido considerado la principal fuente de verdad en el desarrollo de software. Los documentos de requisitos tienden a desactualizarse, los diagramas de diseño quedan obsoletos y, en muchos proyectos, el comportamiento real del sistema sólo puede comprenderse leyendo el código.

El **Spec-Driven Development (SDD)** propone invertir este enfoque tradicional: la especificación pasa a ser la fuente primaria de verdad, mientras que el código se convierte en un artefacto derivado que implementa dicha especificación.

En lugar de escribir código primero y documentarlo después —o no documentarlo— los equipos definen inicialmente especificaciones claras del comportamiento esperado. Posteriormente, el código se genera, implementa o valida frente a esas especificaciones.

**Principio central:**

> En SDD, el código es un detalle de implementación de la especificación. La especificación declara la intención; el código la materializa.

---

## 2. El papel catalizador de la Inteligencia Artificial

Aunque el concepto de especificar primero no es nuevo —frameworks como **TDD** o **BDD** ya promovían esta idea— la aparición de asistentes de programación basados en inteligencia artificial ha incrementado significativamente su relevancia.

Los modelos generativos de código funcionan especialmente bien cuando disponen de instrucciones claras y estructuradas. Sin embargo, cuando reciben prompts ambiguos, tienden a completar los detalles mediante suposiciones, lo que puede introducir errores o comportamientos no deseados.

El SDD reduce este problema proporcionando **contratos explícitos y verificables** que delimitan el espacio de solución del modelo de IA.

Herramientas modernas como **GitHub Spec Kit** estructuran este flujo de trabajo mediante fases bien definidas —especificación, planificación, generación de tareas e implementación— permitiendo que los asistentes de IA operen bajo restricciones claras y reduzcan comportamientos no deterministas.

---

## 3. Historia y evolución del Spec-Driven Development

El SDD no representa una innovación repentina, sino la evolución de varias corrientes de ingeniería de software desarrolladas durante décadas.

### 3.1 Orígenes: Design by Contract (años 90)

El antecedente conceptual más claro es **Design by Contract**, introducido por Bertrand Meyer en 1992.

Este paradigma propone que las interfaces de software se definan mediante:

- **Precondiciones**: requisitos que deben cumplirse antes de ejecutar una operación
- **Postcondiciones**: garantías que el sistema ofrece tras ejecutarla
- **Invariantes**: propiedades que deben mantenerse siempre

Aunque el enfoque introdujo una forma rigurosa de especificar comportamiento, en muchos proyectos los documentos de diseño (HLD, LLD o especificaciones de requisitos) terminaban desincronizándose del código debido a presiones de entrega y evolución continua del sistema.

---

### 3.2 La era ágil: TDD y BDD (años 2000)

Para reducir esta desincronización surgieron prácticas ágiles que integraban la especificación dentro del propio proceso de desarrollo.

**Test-Driven Development (TDD)**

- Las pruebas se escriben antes que el código.
- Cada prueba actúa como una micro-especificación del comportamiento esperado.

**Behavior-Driven Development (BDD)**

BDD extendió esta idea mediante el uso de lenguaje natural estructurado (por ejemplo, **Gherkin**):

```
Given a user with a valid account
When the user logs in
Then the system grants access
```

Este enfoque permite que tanto stakeholders como desarrolladores acuerden el comportamiento del sistema antes de implementar el código.

---

### 3.3 La era de las APIs: Design-First (años 2010)

La proliferación de arquitecturas de microservicios impulsó el enfoque **API-First** o **Design-First**.

En este modelo, el contrato de servicio se define previamente mediante especificaciones como:

- OpenAPI / Swagger
- GraphQL schemas
- Protocol Buffers

Definir el contrato antes de la implementación permite que distintos equipos trabajen en paralelo (por ejemplo, frontend y backend) y reduce significativamente los problemas de integración.

---

### 3.4 El renacimiento con la IA (actualidad)

Con la llegada de la programación asistida por IA, el cuello de botella del desarrollo ha cambiado.

Si una IA puede generar código rápidamente, el verdadero desafío pasa a ser **especificar correctamente qué código debe generarse**.

Los primeros experimentos con IA generativa popularizaron el llamado **"vibe coding"**, donde los desarrolladores daban instrucciones vagas esperando que el modelo completara los detalles. El resultado solía ser código funcional pero lleno de supuestos incorrectos.

El SDD moderno aborda este problema convirtiendo la especificación en un **contrato ejecutable**, validado automáticamente mediante pruebas y pipelines de integración continua.

---

## 4. Niveles de rigor en Spec-Driven Development

El SDD no es una metodología única y rígida. En la práctica existe un espectro de adopción que puede clasificarse en tres niveles principales.

### 4.1 Spec-First

**Definición**  
La especificación se escribe antes de la implementación para guiar el desarrollo inicial.

**Características**

- Proporciona un punto de partida claro para asistentes de IA.
- El código termina convirtiéndose en el artefacto principal.
- Existe riesgo de divergencia entre especificación y código.

**Casos de uso típicos**

- prototipos
- pruebas de concepto
- desarrollos rápidos asistidos por IA

---

### 4.2 Spec-Anchored

**Definición**  
La especificación se mantiene sincronizada con el código durante todo el ciclo de vida del sistema.

**Características**

- Las pruebas automatizadas verifican que la implementación cumple la especificación.
- Si existe divergencia entre ambos artefactos, las pruebas fallan.
- Actúa como documentación viva del sistema.

**Ejemplos habituales**

- BDD con Cucumber
- APIs definidas con OpenAPI y verificadas mediante contract testing

Este nivel suele considerarse el **equilibrio óptimo** para sistemas en producción.

---

### 4.3 Spec-as-Source

**Definición**  
La especificación es el único artefacto que los desarrolladores editan directamente.

El código se genera automáticamente a partir de ella y **no debe modificarse manualmente**.

**Características**

- elimina completamente el riesgo de "drift"
- cualquier cambio requiere modificar la especificación
- el código se regenera automáticamente

**Dominios donde es común**

- generación de servidores a partir de OpenAPI
- sistemas embebidos model-based
- generación de código C desde modelos de Simulink

Este enfoque requiere una elevada madurez de las herramientas de generación.

---

## 5. Recursos recomendados

Para profundizar en el Spec-Driven Development y su aplicación en entornos modernos de desarrollo asistido por IA, se pueden consultar los siguientes recursos:

- GitHub Blog — _Spec-Driven Development with AI_
- GitHub Spec Kit Documentation
- Martin Fowler — _Exploring Gen AI: SDD Tools_
- [NotebookLM sobre SDD](https://notebooklm.google.com/notebook/593d7cbc-e8c2-4385-bfe6-df26bb156f0e)

Estos materiales describen herramientas, patrones de trabajo y ejemplos prácticos de implementación del enfoque SDD en proyectos reales.


# Requerimientos del Sistema - Bankify

## Requerimientos Funcionales 

| #     | Descripción |
|-------|-------------|
| **1** | El sistema debe permitir la autenticación de clientes y operadores mediante usuario y contraseña. |
| **2** | El sistema debe permitir a los supervisores crear, activar, inactivar y actualizar la información de los clientes. |
| **3** | El sistema debe permitir a los asesores crear, activar, inactivar y actualizar cuentas bancarias, y a los clientes inactivar sus propias cuentas. |
| **4** | El sistema debe permitir a los clientes consultar el saldo de sus cuentas y realizar depósitos. |
| **5** | El sistema debe generar reportes tributarios en PDF para los clientes y en JSON para la DIAN. |

## Requerimientos No Funcionales 

| #     | Descripción |
|-------|-------------|
| **1** | El sistema debe validar que los números de cuenta tengan exactamente 10 dígitos numéricos. |
| **2** | El sistema debe validar que los dos primeros dígitos del número de cuenta correspondan a un banco registrado. |
| **3** | El sistema debe garantizar que solo usuarios autenticados y autorizados accedan a las funcionalidades según su rol. |
| **4** | El sistema debe generar los reportes en un tiempo máximo de 5 segundos. |
| **5** | El sistema debe registrar en un log todas las operaciones críticas (creación, inactivación, eliminación, depósitos). |

# Detalle de Requerimientos Funcionales - Bankify

## Caso de Uso 1: Gestionar Cuentas

| Aspecto | Descripción |
|---------|-------------|
| **Nombre** | Gestionar Cuentas Bancarias |
| **Código** | RF-GC-01 |
| **Descripción general** | El sistema debe permitir la administración de cuentas bancarias, donde los asesores pueden realizar todas las operaciones y los usuarios (clientes) pueden inactivar sus propias cuentas. |
| **Actores** | Asesor, Usuario (Cliente) |
| **Prioridad** | Alta |

### Sub-casos de uso incluidos:

**1. Crear cuenta bancaria**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Asesor |
| **Descripción** | Permite crear una nueva cuenta bancaria para un cliente existente |
| **Precondiciones** | - Asesor autenticado<br>- Cliente existente y activo<br>- Banco registrado en el sistema |
| **Flujo principal** | 1. Asesor ingresa al módulo de cuentas<br>2. Selecciona "Crear cuenta"<br>3. Busca y selecciona el cliente<br>4. Selecciona el banco (define primeros 2 dígitos)<br>5. Sistema genera automáticamente los 8 dígitos restantes<br>6. Sistema valida que el número sea único<br>7. Asesor confirma la creación<br>8. Sistema activa la cuenta por defecto |
| **Postcondiciones** | Cuenta creada y asociada al cliente con estado "Activa" |
| **Reglas de negocio** | - Número de cuenta: 10 dígitos numéricos<br>- Dígitos 1-2: código de banco válido |

**2. Activar cuenta bancaria**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Asesor |
| **Descripción** | Permite activar una cuenta bancaria que estaba inactiva |
| **Precondiciones** | - Asesor autenticado<br>- Cuenta existente y en estado "Inactiva" |
| **Flujo principal** | 1. Asesor busca la cuenta<br>2. Selecciona "Activar cuenta"<br>3. Sistema solicita confirmación<br>4. Asesor confirma la acción<br>5. Sistema cambia estado a "Activa" |
| **Postcondiciones** | Cuenta con estado "Activa" (habilita operaciones) |

**3. Inactivar cuenta bancaria**
| Campo | Descripción |
|-------|-------------|
| **Actores** | Asesor, Usuario (Cliente - solo cuentas propias) |
| **Descripción** | Permite desactivar una cuenta bancaria existente |
| **Precondiciones** | - Usuario autenticado<br>- Cuenta existente y activa<br>- Usuario (cliente): solo puede inactivar sus propias cuentas |
| **Flujo principal** | 1. Usuario busca la cuenta<br>2. Selecciona "Inactivar cuenta"<br>3. Sistema solicita confirmación<br>4. Usuario confirma la acción<br>5. Sistema cambia estado a "Inactiva" |
| **Postcondiciones** | Cuenta con estado "Inactiva" (no permite operaciones) |

**4. Actualizar información de cuenta**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Asesor |
| **Descripción** | Permite modificar datos de una cuenta bancaria existente |
| **Precondiciones** | - Asesor autenticado<br>- Cuenta existente |
| **Flujo principal** | 1. Asesor busca la cuenta<br>2. Selecciona "Editar cuenta"<br>3. Modifica los campos permitidos<br>4. Sistema valida los cambios<br>5. Asesor confirma la actualización<br>6. Sistema guarda los cambios |
| **Postcondiciones** | Información de cuenta actualizada |

---

## Caso de Uso 2: Consultar Reportes

| Aspecto | Descripción |
|---------|-------------|
| **Nombre** | Consultar Reportes Tributarios |
| **Código** | RF-CR-02 |
| **Descripción general** | El sistema debe permitir la generación y consulta de reportes tributarios en diferentes formatos según el usuario. |
| **Actores** | Usuario (Cliente), Asesor |
| **Prioridad** | Media |

### Sub-casos de uso incluidos:

**1. Generar reporte PDF para cliente**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Usuario (Cliente) |
| **Descripción** | Permite al cliente generar un reporte tributario en PDF con el resumen de sus movimientos para declaración de renta |
| **Precondiciones** | - Usuario autenticado como cliente<br>- Cliente tiene al menos una cuenta activa<br>- Hay movimientos en el período seleccionado |
| **Flujo principal** | 1. Cliente ingresa al módulo de reportes<br>2. Selecciona "Reporte tributario individual"<br>3. Selecciona el año gravable<br>4. Sistema calcula:<br>   - Total de ingresos (depósitos)<br>   - Saldo promedio<br>   - Intereses generados (si aplica)<br>5. Sistema genera archivo PDF<br>6. Cliente puede descargar o enviar por email |
| **Contenido del reporte** | - Información del cliente<br>- Cuentas asociadas<br>- Resumen de movimientos del año<br>- Totales y valores tributarios |
| **Postcondiciones** | Reporte PDF generado y disponible para el cliente |

**2. Generar reporte JSON para DIAN**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Asesor (con rol de Gerente Financiero) |
| **Descripción** | Permite generar un reporte consolidado en formato JSON con la información de todas las cuentas para enviar a la DIAN |
| **Precondiciones** | - Asesor con permisos de gerente financiero autenticado<br>- Hay información de cuentas en el sistema |
| **Flujo principal** | 1. Asesor ingresa al módulo de reportes<br>2. Selecciona "Reporte DIAN"<br>3. Selecciona el período a reportar<br>4. Sistema consolida información de todas las cuentas activas<br>5. Sistema genera archivo JSON con estructura definida<br>6. Asesor descarga el archivo<br>7. Sistema registra la generación del reporte |
| **Estructura del JSON** | ```json
{
"entidad": "Bankify",
"periodo": "2024",
"total_cuentas": 150,
"clientes": [
{
"id": "12345",
"nombre": "Cliente X",
"cuentas": []
}
]
}
``` |
| **Postcondiciones** | Reporte JSON generado y listo para enviar a la DIAN |
| **Reglas de negocio** | - El formato debe cumplir especificaciones DIAN<br>- Debe incluir todas las cuentas activas del período |

**3. Consultar reportes generados**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Usuario, Asesor |
| **Descripción** | Permite consultar el historial de reportes generados previamente |
| **Precondiciones** | - Usuario autenticado<br>- Existen reportes generados anteriormente |
| **Flujo principal** | 1. Usuario ingresa al módulo de reportes<br>2. Selecciona "Historial de reportes"<br>3. Sistema muestra listado de reportes generados<br>4. Usuario puede visualizar o descargar nuevamente |
| **Postcondiciones** | Usuario accede a reportes históricos |

---

## Caso de Uso 3: Consultar Movimientos

| Aspecto | Descripción |
|---------|-------------|
| **Nombre** | Consultar Movimientos de Cuenta |
| **Código** | RF-CM-03 |
| **Descripción general** | El sistema debe permitir la consulta del historial de movimientos de las cuentas bancarias. |
| **Actores** | Usuario (Cliente), Asesor |
| **Prioridad** | Alta |

### Sub-casos de uso incluidos:

**1. Consultar movimientos de cuenta propia**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Usuario (Cliente) |
| **Descripción** | Permite al cliente consultar el historial de movimientos de sus propias cuentas |
| **Precondiciones** | - Cliente autenticado<br>- Cliente tiene al menos una cuenta activa |
| **Flujo principal** | 1. Cliente ingresa al módulo de movimientos<br>2. Selecciona la cuenta a consultar<br>3. Sistema muestra listado de movimientos recientes<br>4. Cliente puede filtrar por fechas o tipo de movimiento<br>5. Sistema actualiza la visualización según filtros |
| **Información mostrada** | - Fecha y hora del movimiento<br>- Tipo (depósito, consulta)<br>- Monto<br>- Saldo después del movimiento |
| **Postcondiciones** | Cliente visualiza el historial de movimientos |

**2. Consultar movimientos de cualquier cuenta (Asesor)**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Asesor |
| **Descripción** | Permite al asesor consultar el historial de movimientos de cualquier cuenta de cliente |
| **Precondiciones** | - Asesor autenticado<br>- Cuenta existente y activa |
| **Flujo principal** | 1. Asesor ingresa al módulo de consultas<br>2. Busca al cliente o número de cuenta<br>3. Selecciona la cuenta deseada<br>4. Sistema muestra historial completo de movimientos<br>5. Asesor puede filtrar y exportar la información |
| **Flujos alternativos** | - Cuenta inactiva: el sistema informa pero permite consultar historial<br>- Cliente no existe: mensaje de error |
| **Postcondiciones** | Asesor obtiene la información requerida |

**3. Exportar movimientos**
| Campo | Descripción |
|-------|-------------|
| **Actor** | Usuario, Asesor |
| **Descripción** | Permite exportar el listado de movimientos a formato PDF o Excel |
| **Precondiciones** | - Usuario autenticado<br>- Hay resultados de movimientos para exportar |
| **Flujo principal** | 1. Usuario realiza una consulta de movimientos<br>2. Selecciona opción "Exportar"<br>3. Elige formato (PDF/Excel)<br>4. Sistema genera archivo<br>5. Usuario descarga el archivo |
| **Postcondiciones** | Archivo exportado disponible para descarga |

---

## Matriz de trazabilidad por actor

| Actor | Casos de Uso | Acciones permitidas |
|-------|--------------|---------------------|
| **Usuario (Cliente)** | Gestionar Cuentas | - Inactivar cuentas propias |
| | Consultar Reportes | - Generar reporte PDF individual<br>- Consultar historial de reportes |
| | Consultar Movimientos | - Consultar movimientos de cuentas propias<br>- Exportar movimientos |
| **Asesor** | Gestionar Cuentas | - Crear cuentas<br>- Activar cuentas<br>- Inactivar cuentas<br>- Actualizar cuentas |
| | Consultar Reportes | - Generar reporte JSON para DIAN<br>- Consultar reportes de clientes |
| | Consultar Movimientos | - Consultar movimientos de cualquier cuenta<br>- Exportar movimientos |

---

## Requerimientos No Funcionales asociados

| Código | Descripción | Casos de Uso afectados |
|--------|-------------|------------------------|
| **RNF-01** | Validar que los números de cuenta tengan exactamente 10 dígitos numéricos | Gestionar Cuentas (crear) |
| **RNF-02** | Validar que los dos primeros dígitos correspondan a un banco registrado | Gestionar Cuentas (crear) |
| **RNF-03** | Garantizar que solo usuarios autenticados y autorizados accedan según su rol | Todos los casos de uso |
| **RNF-04** | Generar reportes en un tiempo máximo de 5 segundos | Consultar Reportes |
| **RNF-05** | Registrar en log todas las operaciones críticas | Gestionar Cuentas (todas), Consultar Reportes (generación) |


# 7. Análisis de Requerimientos

## a. ¿Identifica algún requerimiento que deba detallarse más? ¿cuál(es)?

Sí, identifico varios requerimientos que necesitan más detalle:

El requerimiento de generar reportes tributarios en PDF para clientes y JSON para la DIAN necesita especificar qué información debe contener cada reporte, la estructura exacta del JSON para que la DIAN lo acepte, y si los reportes son anuales, mensuales o por período personalizado.

El requerimiento de realizar depósitos debería detallar si hay montos mínimos o máximos por transacción y qué métodos de pago se aceptan (efectivo, transferencia, etc.).

El requerimiento de que los clientes puedan inactivar sus propias cuentas no especifica si se requiere alguna confirmación adicional, qué pasa con el saldo de la cuenta al inactivarla, o si el cliente puede reactivarla después.

## b. ¿Existen requerimientos que se contradigan entre sí? ¿cuál(es)?

Sí, encuentro algunas contradicciones:

Entre el requerimiento de que los clientes puedan inactivar sus propias cuentas y el de eliminar clientes con todas sus cuentas asociadas hay una posible contradicción. Si un cliente inactiva su cuenta pero luego el supervisor quiere eliminar al cliente, no queda claro si se puede eliminar un cliente que tiene cuentas inactivas o si primero deben reactivarse.

También hay ambigüedad en quién puede hacer depósitos en cuentas de otros clientes. El enunciado dice "otros usuarios" pero no especifica si cualquier usuario autenticado puede hacerlo o solo roles específicos como asesores.

Otra posible contradicción es entre generar el reporte JSON para DIAN que consolida todas las cuentas y el tiempo máximo de 5 segundos para generar reportes. Con muchos clientes, consolidar toda la información en menos de 5 segundos puede ser técnicamente difícil.

## c. Si tuviera que dar una prioridad a los requerimientos, ¿cuáles deberían ser los 2 más importantes que deberían implementarse en una primera iteración del proyecto?

Para una primera iteración del proyecto, los dos requerimientos más importantes serían:

El primero es la gestión de cuentas, específicamente la creación de cuentas, porque sin cuentas no hay operaciones posibles. Los asesores necesitan poder registrar clientes y crear sus cuentas bancarias con las validaciones de 10 dígitos y banco registrado.

El segundo es la consulta de saldo y depósitos, porque es la funcionalidad principal que los clientes esperan de un banco: poder ver su dinero y agregar más. Esto permite validar el modelo de negocio con usuarios reales desde el principio.

Las demás funcionalidades como autenticación avanzada, reportes tributarios y eliminación de clientes pueden venir en iteraciones posteriores.

## d. ¿Existe algún requerimiento que no debería realizarse?

Sí, considero que el requerimiento de "eliminar un cliente y las cuentas que tenga asociadas" no debería implementarse tal como está planteado.

En el sector financiero, por normativa legal y regulatoria, los datos de clientes y sus transacciones deben conservarse por varios años, generalmente entre 5 y 10 años, para efectos de auditoría y cumplimiento con entidades como la DIAN. Eliminar esta información podría violar estas normas y generar problemas legales para Bankify.

Lo recomendable sería reemplazar "eliminar" por "inactivar" al cliente, manteniendo sus datos históricos pero restringiendo el acceso y las operaciones. Así se cumple con las leyes, se conserva la trazabilidad y se evitan problemas legales en el futuro.
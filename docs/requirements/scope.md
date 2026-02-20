# Alcance del Sistema - Diagrama de Contexto

## Sistema
**Bankify**: Plataforma fintech MVP para gestión básica de cuentas bancarias.

## Problema a Resolver
Bankify no tiene sistema centralizado para:
- Registrar/validar cuentas (10 dígitos numéricos, 2 primeros = código banco registrado)
- Consultar saldo de cuentas
- Realizar depósitos controlados
- Generar reportes tributarios (PDF clientes, JSON DIAN)

## Diagrama de Contexto
![Diagrama de Contexto](./../uml/diagrama-contexto-bankify.png)

**Enlace editable**: [Draw.io Link - pega tu enlace aquí]

**Actores identificados**:
- Cliente: Autenticación, saldo, depósitos, PDF
- Asesor/Operador: CRUD clientes/cuentas
- Supervisor/Gerente: CRUD + reportes DIAN
- DIAN: Recepción JSON
- Bancos: Validación códigos

## Alcance del Sistema
### INCLUYE (MVP):
- Autenticación usuario/contraseña
- Gestión clientes (CRUD por roles)
- Gestión cuentas (CRUD por roles)
- Consulta saldo
- Depósitos
- Reportes tributarios (PDF/JSON)

### EXCLUYE:
- Transferencias entre cuentas
- Préstamos/inversiones
- Integración real-time bancos
- Pagos móviles

### Límites:
- Validación reglas negocio básica
- Reportes formato fijo (PDF/JSON)
- Sin escalabilidad alta (MVP)

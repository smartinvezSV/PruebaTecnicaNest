# Prueba Técnica Backend - Sistema de Gestión de Empleados

## Contexto del Negocio

Eres el desarrollador backend de **TalentHub**, una empresa de gestión de recursos humanos que ayuda a otras compañías a administrar sus empleados. La plataforma permite a las empresas cliente registrar sus empleados, gestionar departamentos y generar reportes.

## Objetivo General

Desarrollar una API REST con NestJS que permita a las empresas cliente gestionar su información de empleados de manera eficiente y segura.

## Stack Tecnológico Requerido

- **Framework**: NestJS (última versión estable)
- **ORM**: Prisma
- **Base de Datos**: PostgreSQL
- **Autenticación**: JWT
- **Lenguaje**: TypeScript
- **Procesamiento de archivos**: Para Excel (xlsx)

## Funcionalidades Requeridas

### 1. Sistema de Autenticación

- **Registro de empresas**: Endpoint para que nuevas empresas se registren
- **Login de empresas**: Autenticación con email y contraseña
- **Protección de rutas**: Middleware JWT para proteger endpoints privados

### 2. Gestión de Departamentos

- **CRUD completo** de departamentos
- Cada departamento debe tener: nombre, descripción, empresa_id
- Solo la empresa propietaria puede gestionar sus departamentos

### 3. Gestión de Empleados

- **CRUD completo** de empleados
- **Carga masiva**: Endpoint para subir archivo Excel con información de empleados
- **Filtros y búsqueda**: Por departamento, estado activo/inactivo, rango de fechas de contratación
- **Validaciones**: Email único por empresa, datos obligatorios

## Modelado de Base de Datos - Consideraciones Importantes

⚠️ **IMPORTANTE**: Antes de implementar, diseña cuidadosamente el modelo de base de datos considerando:

1. **Relaciones entre entidades**:

   - ¿Cómo se relacionan las empresas con sus empleados?
   - ¿Un departamento puede existir sin empleados?
   - ¿Un empleado puede cambiar de departamento? ¿Cómo manejarías el historial?

2. **Integridad de datos**:

   - ¿Qué restricciones de unicidad necesitas?
   - ¿Qué campos son obligatorios vs opcionales?
   - ¿Cómo garantizas que una empresa solo vea sus propios datos?

3. **Escalabilidad**:

   - ¿Qué índices necesitarías para consultas eficientes?
   - ¿Cómo optimizarías las consultas de reportes?

4. **Auditoría**:
   - ¿Necesitas timestamps de creación/actualización?
   - ¿Cómo manejarías eliminaciones lógicas vs físicas?

## Endpoints Principales a Implementar

### Autenticación

```
POST /auth/register     # Registro de empresa
POST /auth/login        # Login
```

### Departamentos

```
GET    /departments           # Listar departamentos de la empresa
POST   /departments           # Crear departamento
PATCH    /departments/:id     # Actualizar departamento
DELETE /departments/:id       # Eliminar departamento
```

### Empleados

```
GET    /employees             # Listar empleados con filtros
POST   /employees             # Crear empleado individual
PATCH    /employees/:id       # Actualizar empleado
DELETE /employees/:id         # Eliminar empleado
POST   /employees/upload      # Carga masiva desde Excel
```

## Criterios de Evaluación

### Código y Arquitectura (30%)

- Estructura limpia del proyecto NestJS
- Uso adecuado de decoradores y módulos
- Separación de responsabilidades (Controllers, Services, DTOs)
- Manejo de errores y validaciones

### Base de Datos (25%)

- Diseño eficiente del modelo de datos
- Uso correcto de Prisma Schema
- Relaciones bien definidas
- Migraciones apropiadas

### Seguridad (20%)

- Implementación correcta de JWT
- Validación y sanitización de datos
- Protección contra inyecciones
- Autorización por empresa

### Funcionalidades (25%)

- Todos los endpoints funcionan correctamente
- Carga de Excel funciona sin errores
- Filtros y búsquedas implementados
- Manejo adecuado de archivos

## Entregables

1. **Código fuente** en repositorio Git
2. **README.md** con:
   - Instrucciones de instalación
   - Comandos para ejecutar el proyecto
   - Estructura de la base de datos
   - Ejemplos de uso de la API
3. **Archivo SQL** con datos de prueba
4. **Archivo Excel** de ejemplo para testing
5. **Documentación** de la API (Swagger)

## Instrucciones Adicionales

1. **Base de datos**: Incluye un docker-compose.yml para PostgreSQL
2. **Variables de entorno**: Usa un archivo .env.example
3. **Logging**: Implementa logging apropiado
4. **Documentación**: Comenta el código únicamente donde sea necesario

## Desafíos Adicionales (Bonus)

Si terminas antes del tiempo estimado o quieres demostrar habilidades avanzadas, considera implementar:

### Autenticación Avanzada

- **Refresh token**: Implementar renovación de tokens JWT
- **Rate limiting**: Limitar intentos de login fallidos

### Reportes y Estadísticas

- **Resumen por empresa**: Total de empleados, empleados por departamento
- **Empleados por rango de fechas**: Filtrar por fecha de contratación
- **Exportar datos**: Endpoint para descargar información en formato JSON

### Endpoints Bonus

```
POST /auth/refresh              # Renovar token
GET  /reports/summary           # Resumen de la empresa
GET  /reports/employees-by-date # Empleados por rango de fechas
GET  /reports/export            # Exportar datos
```

### Optimizaciones

- **Paginación** en listados de empleados
- **Validación avanzada** de archivos Excel
- **Cache** para consultas frecuentes
- **Notificaciones** por email al completar carga masiva
- **Tests de integración** con base de datos en memoria
- **Despliegue en Railway**: Configurar y desplegar la aplicación en Railway con PostgreSQL

## Preguntas para Reflexión

Al finalizar, prepárate para discutir:

1. ¿Por qué elegiste esta estructura de base de datos?
2. ¿Cómo manejarías el crecimiento a millones de empleados?
3. ¿Qué optimizaciones implementarías para mejorar performance?
4. ¿Cómo asegurarías la consistencia de datos en cargas masivas?
5. ¿Qué estrategia usarías para el manejo de errores en el procesamiento de Excel?

---

**¡Buena suerte y que demuestres tus habilidades como desarrollador backend!** 🚀

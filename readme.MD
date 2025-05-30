# Microservicios - Sistema de Gestión de Flota

## 1. gestionUsuario()

**Responsabilidad**: Administrar usuarios del sistema. Relaciona con: AUTH, gestionarClientes(), gestionarFlota()

### Model

- Usuario (id_usuario, nombre, email, contraseña, id_rol)
- Rol (id_rol, nombre_rol)

### Repository

- UsuarioRepository
- RolRepository

### Service

- UsuarioService (crearUsuario, actualizarUsuario, eliminarUsuario, listarPorRol)
- AuthService (login, validación, generación de tokens)

### Controller

Nombre Controller: UsuarioController

- POST /usuarios
- GET /usuarios/{id}
- PUT /usuarios/{id}
- DELETE /usuarios/{id}
- GET /usuarios?rol=ADMIN

---

## 2. gestionarCliente()

**Responsabilidad**: Gestionar clientes de la empresa. Relaciona con: gestionarCarga(), gestionarRuta()

### Model

- Empresa (id_emp, nombre_emp, rut_emp, dv_emp, dir_emp)
- Cliente (id_cli, nombre_cli, apellido_cli, run_cli, dv_cli, origen_cli, destino_cli, tel_cli)

### Repository

- ClienteRepository CRUD
- EmpresaRepository CRUD

### Service

- EmpresaService (CRUD + obtenerClientesPorEmpresa)
- ClienteService

### Controller

EmpresaController api/v1/empresas

- GET /empresas: listar todas las empresas
- GET /empresas/{id_emp}: obtener una empresa por ID
- POST /empresas: crear empresa
- PUT /empresas/{id_emp}: actualizar empresa
- DELETE /empresas/{id_emp}: eliminar empresa

ClienteController api/v1/empresas/{id_emp}/clientes

(Clientes anidados bajo una empresa)

- GET /empresas/{id_emp}/clientes: obtener todos los clientes de una empresa
- GET /empresas/{id_emp}/clientes/{id_cli}: obtener cliente específico de esa empresa
- POST /empresas/{id_emp}/clientes: crear cliente para una empresa
- PUT /empresas/{id_emp}/clientes/{id_cli}: actualizar cliente
- DELETE /empresas/{id_emp}/clientes/{id_cli}: eliminar cliente

---

## 3. Empresa()

**Responsabilidad**: Gestionar clientes de la empresa.

### Model

- Empresa (id_emp, nombre_emp, rut_emp, dv_emp, dir_emp)

### Repository

- EmpresaRepository CRUD

### Service

- EmpresaService (CRUD + obtenerClientesPorEmpresa)

### Controller

EmpresaController api/v1/empresas

- GET /empresas: listar todas las empresas
- GET /empresas/{id_emp}: obtener una empresa por ID
- POST /empresas: crear empresa
- PUT /empresas/{id_emp}: actualizar empresa
- DELETE /empresas/{id_emp}: eliminar empresa

---

## 4. gestionarCarga()

**Responsabilidad**: Administración de cargas y guías de despacho. Relaciona con: gestionarRuta(), Conductor

### Model

- Carga (id, descripcion)
- GuiaCliente (id, id_cliente, id_ruta, id_carga)

### Repository

- CargaRepository
- GuiaClienteRepository

### Service

- CargaService (crearCarga, actualizar, eliminar, cambiarEstado)
- GuiaClienteService (crearGuia, consultarGuia)

### Controller

Nombre Controller: CargaController

- POST /cargas
- GET /cargas/{id_carga}
- PUT /cargas/{id_carga}
- DELETE /cargas/{id_carga}

Nombre Controller: GuiaClienteController

- POST /guias-cliente
- GET /guias-cliente/{id_guia}

---

## 5. Ruta()

**Responsabilidad**: Crear, asignar y calcular rutas. Relaciona con: gestionarCarga(), gestionarFlota()

### Model

- Ruta (origen, destino, distancia_km, tiempo_estimado)
- Parada (id_ruta, ubicación, orden)

### Repository

- RutaRepository
- ParadaRepository

### Service

- RutaService (crearRuta, actualizarRuta, eliminarRuta)

### Controller

RutaController api/v1/rutas

- POST /rutas
- GET /rutas/{id_ruta}
- PUT /rutas/{id_ruta}
- DELETE /rutas/{id_ruta}

---

## 6. gestionEntrada()

**Responsabilidad**: Iniciar un viaje.

### Model

- iniciarViaje (id_viaje, hora_inicio, km_actual, id_conductor, id_vehiculo)

### Repository

- iniciarViajeRepository

### Service

- iniciarViaje(id_conductor)

### Controller

iniciarViajeController api/v1/viaje/iniciar/{id_conductor}

- POST /viaje/iniciar/{id_conductor}

---

## 7. gestionSalida()

**Responsabilidad**: Finalizar un viaje.

### Model

- terminarViaje (id_viaje, hora_termino, km_final, id_conductor, id_vehiculo)

### Repository

- terminarViajeRepository

### Service

- terminarViaje(id_conductor)

### Controller

terminarViajeController api/v1/viaje/terminar/{id_conductor}

- POST /viaje/terminar/{id_conductor}

---

## 8. gestionPago()

**Responsabilidad**: Revision de pago

### Model

- egestionPago

### Repository

- gestionPagoRepository

### Service

- gestionPagoService

### Controller

estadoCargaController api/v1/pago

- POST /pagos
- GET /pagos
- Get /pagos/{id}
- Put /pagos/{id}
- Delete /pagos/{id}

---

## 9. AuthService()

**Responsabilidad**: Validacion de rol ADmin.

### Model

- Authservice

### Repository

- AuthserviceRepository

### Service

- AuthserviceService

### Controller

- AuthserviceController /auth

- POST /verificar-admin

---

## 10. Vehiculo()

**Responsabilidad**: Aisgnacion de vehiculos

### Model

- vehiculo{iid, patente, estado, km_actual}

### Repository

- vehiculoRepository{obtener, guardar,eliminar buscarporId, actualizar}

### Service

- Service {vehiculoRepository}

### Controller

VehiculoController api/v1/vehiculos

- POST /vehiculos
- GET /vehiculos
- Put /vehiculos/{id}
- Eliminar /vehiculos/{id}

---

## 11. reporteGeneral()

**Responsabilidad**: Crear reportes.

### Model

- reporte (id_reporte, nombre_cliente, apellido_cliente, nombre_empresa, rut_empresa, nombre_conductor, hora_reporte, fecha_reporte, patente_vehiculo, observacion, id_viaje, estado_carga)

### Repository

- reporteRepository

### Service

- ReporteService (generarReporte()) hacer validaciones y llamar microservicios
- listarReportes()

### Controller

SistemaController api/v1/reportes

- POST /reportes
- GET /reportes/{id_reporte}

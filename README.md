# Modelo Entidad-Relación para la Gestión de una Farmacia

## Entidades

### 1. Medicamento
- **Descripción**: Representa los medicamentos disponibles en la farmacia, incluyendo los detalles necesarios para su catalogación, control de stock y ventas.
- **Atributos**:
  - `Código_medicamento` (entero): Identificador único del medicamento. Ejemplo: `123456789`
  - `Nombre` (cadena de caracteres): Nombre comercial del medicamento. Ejemplo: `Paracetamol`
  - `Tipo` (cadena de caracteres): Forma farmacéutica del medicamento (jarabe, comprimido, pomada, etc.). Ejemplo: `Comprimido`
  - `Stock` (entero): Número de unidades disponibles en el inventario. Ejemplo: `200`
  - `Unidades_Vendidas` (entero): Número de unidades vendidas totales de un medicamento concreto. Ejemplo: `150`
  - `Precio_total` (decimal, calculado): Precio total del medicamento, es decir, añadiendo impuestos. Ejemplo: `5.50`
  - `Receta_médica` (booleano): Indica si el medicamento requiere receta médica para su venta. Ejemplo: `true` o `false`

### 2. Laboratorio
- **Descripción**: Representa a los laboratorios que suministran algunos de los medicamentos vendidos en la farmacia (existen medicamentos que los hace la misma farmacia).
- **Atributos**:
  - `Código_Laboratorio` (entero): Identificador único del laboratorio. Ejemplo: `123456789`
  - `Nombre` (cadena de caracteres): Nombre del laboratorio. Ejemplo: `Laboratorios Farma`
  - `Teléfono` (cadena de caracteres, multievaluado): Número de teléfono de contacto del laboratorio. Ejemplo: `+34 912345678`
  - `Dirección_Postal` (cadena de caracteres): Dirección completa del laboratorio. Ejemplo: `Calle Mayor, 10, 28013`
  - `Fax` (cadena de caracteres, multievaluado): Número de fax del laboratorio. Ejemplo: `+34 912345679`
  - `Persona_Contacto` (cadena de caracteres): Nombre de la persona de contacto en el laboratorio. Ejemplo: `Carlos García`

### 3. Familia
- **Descripción**: Clasificación de los medicamentos en función del tipo de enfermedad o condición para la que se utilizan.
- **Atributos**:
  - `Código_Familia` (entero): Identificador único de la familia. Ejemplo: `123456789`
  - `Nombre` (cadena de caracteres): Nombre de la familia de medicamentos. Ejemplo: `Analgésicos`
  - `Enfermedades` (cadena de caracteres, multievaluado): Enfermedades o condiciones que trata. Ejemplo: `Dolor de cabeza, catarro...`

### 4. Cliente con crédito
- **Descripción**: Representa a los clientes de la farmacia **con crédito**.
- **Atributos**:
  - `DNI` (cadena de caracteres): DNI del cliente. Ejemplo: `79151744V`
  - `Nombre` (cadena de caracteres): Nombre completo del cliente. Ejemplo: `Ana López`
  - `Teléfono` (cadena de caracteres, multievaluado): Número de teléfono del cliente. Ejemplo: `+34 912345680`
  - `Email` (cadena de caracteres, multievaluado): Dirección de correo electrónico del cliente. Ejemplo: `analopez@gmail.com`
  - `Fecha_de_pago` (entero): Fecha en la que paga el cliente cada mes. Ejemplo: `25` (día 25 de cada mes)
  - `IBAN` (cadena de caracteres): Código IBAN de la cuenta bancaria del cliente. Ejemplo: `ES91 2100 0418 4502 0005 1332`
 
### 5. Pedido
- **Descripción**: Representa los pedidos (venta de medicamentos) realizadas por clientes con o sin crédito.
- **Atributos**:
  - `Código_pedido` (entero): Identificador único del pedido. Ejemplo: `123456789`
  - `Unidades` (entero): Cantidad de medicamentos vendidos. Ejemplo: `3`
  - `Fecha_de_pedido` (fecha): Fecha en la que se realizó el pedido. Ejemplo: `02/03/2023`
  
## Relaciones

### 1. Medicamento (1,N) - (0,N) Laboratorio
- **Descripción**: Un medicamento puede **no** ser suministrado por un laboratorio (lo hace la propia farmacia) o puede ser suministrado por varios. Un laboratorio fabrica uno o más medicamentos.
  - `Fecha_suministración` (fecha): Fecha en la que se suministró el medicamento a la farmacia por el laboratorio. Ejemplo: `02/03/2023`

### 2. Medicamento (1,N) - (1,1) Familia
- **Descripción**: Un medicamento pertenece a una sola familia. Una familia puede agrupar varios medicamentos.

### 3. Medicamento (1,1) - (1,N) Pedido
- **Descripción**: Se pueden hacer múltiples pedidos de un mismo medicamento (que un cliente o varios compren paracetamol) pero un pedido se hace sobre un medicamento (para llevar la cantidad exacta vendida de ese medicamento).

### 4. Cliente con crédito (0,1) - (1,N) Pedido
- **Descripción**: Un cliente con crédito puede estar involucrado en uno o más pedidos y un pedido puede estar asociado a un cliente con crédito o cero (en el caso de que sea un cliente sin crédito).

## Restricciones Semánticas

1. **Medicamento con Receta**: Los medicamentos que requieren receta solo pueden ser vendidos si se adjunta la receta correspondiente en el proceso de venta.
2. **Stock Suficiente**: No se puede realizar una venta si la cantidad de unidades en `Stock` es menor que la cantidad del pedido.
3. El precio, las unidades vendidas totales, el stock y la cantidad de unidades en los pedidos no pueden ser negativos.

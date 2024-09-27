# Modelo Entidad-Relación para la Gestión de una Farmacia

## Entidades

### 1. Medicamento
- **Descripción**: Representa los medicamentos disponibles en la farmacia, incluyendo los detalles necesarios para su catalogación, control de stock y ventas.
- **Atributos**:
  - `Código_Medicamento`: Identificador único del medicamento. Ejemplo: `MED12345`
  - `Nombre`: Nombre comercial del medicamento. Ejemplo: `Paracetamol`
  - `Tipo`: Forma farmacéutica del medicamento (jarabe, comprimido, pomada, etc.). Ejemplo: `Comprimido`
  - `Stock`: Número de unidades disponibles en el inventario. Ejemplo: `200`
  - `Unidades_Vendidas`: Número de unidades vendidas. Ejemplo: `150`
  - `Precio total`: Precio total del medicamento, es decir, añadiendo impuestos. Ejemplo: `5.50` (moneda local)
  - `Requiere_Receta`: Indica si el medicamento requiere receta médica para su venta (`booleano`). Ejemplo: `true`

### 2. Laboratorio
- **Descripción**: Representa a los laboratorios que suministran o fabrican los medicamentos vendidos en la farmacia.
- **Atributos**:
  - `Código_Laboratorio`: Identificador único del laboratorio. Ejemplo: `LAB123`
  - `Nombre`: Nombre del laboratorio. Ejemplo: `Laboratorios Farma`
  - `Teléfono`: Número de teléfono de contacto del laboratorio. Ejemplo: `+34 912345678`
  - `Dirección_Postal`: Dirección completa del laboratorio. Ejemplo: `Calle Mayor, 10, 28013`
  - `Fax`: Número de fax del laboratorio. Ejemplo: `+34 912345679`
  - `Persona_Contacto`: Nombre de la persona de contacto en el laboratorio. Ejemplo: `Carlos García`

### 3. Familia
- **Descripción**: Clasificación de los medicamentos en función del tipo de enfermedad o condición para la que se utilizan.
- **Atributos**:
  - `Código_Familia`: Identificador único de la familia. Ejemplo: `FAM001`
  - `Nombre`: Nombre de la familia de medicamentos. Ejemplo: `Analgésicos`
  - `Enfermedades`: Enfermedades o condiciones que trata. Ejemplo: `Dolor de cabeza, catarro...`

### 4. Cliente
- **Descripción**: Representa a los clientes de la farmacia, diferenciando entre aquellos que pagan al momento de la compra y aquellos con crédito.
- **Atributos**:
  - `DNI`: DNI del cliente. Ejemplo: `79151744V`
  - `Nombre`: Nombre completo del cliente. Ejemplo: `Ana López`
  - `Dirección`: Dirección del cliente. Ejemplo: `Calle del Sol 45, 28080 Madrid, España`
  - `Teléfono`: Número de teléfono del cliente. Ejemplo: `+34 912345680`
  - `Email`: Dirección de correo electrónico del cliente. Ejemplo: `ana.lopez@gmail.com`
  - `Fecha de pago`: Fecha en la paga el cliente cada mes Ejemplo: `28`

## Relaciones

### 1. Medicamento (0,N) - Fabricar - (0,N) Laboratorio
- **Descripción**: Un medicamento puede no ser fabricado por un Laboratorio o puede ser fabricado por varios. Un Laboratorio fabrica uno o más medicamentos.
- **Cardinalidad**: Muchos Medicamentos están asociados a un Laboratorio.

### 2. Medicamento (1,N) - Pertenecer - (1,1) Familia
- **Descripción**: Un medicamento pertenece a una sola familia, que clasifica el medicamento según el tipo de enfermedades que trata. Una familia puede agrupar varios medicamentos.
- **Cardinalidad**: Muchos Medicamentos pertenecen a una Familia.

### 3. Cliente  (1,1) - Comprar - (1,N) Medicamento
- `Fecha de compra`: Fecha en la que se hizo la compra. Ejemplo: `10/12/2024`
- `Cantidad`: Cantidad de medicamentos. Ejemplo: `3`
- **Descripción**: Un cliente puede realizar múltiples compras a lo largo del tiempo, pero cada compra está asociada a un único cliente.
- **Cardinalidad**: Un Cliente puede realizar muchas Compras.

## Restricciones Semánticas

1. **Medicamento con Receta**: Los medicamentos que requieren receta (`Requiere_Receta = true`) solo pueden ser vendidos si se adjunta la receta correspondiente en el proceso de venta.
2. **Stock Suficiente**: No se puede realizar una venta si las `Unidades_En_Stock` son menores que las `Unidades_Compradas` en una transacción.
3. **Unicidad de Código**: Los códigos (`Código_Medicamento`, `Código_Laboratorio`, `Código_Familia`, `Código_Cliente`, `Código_Compra`) deben ser únicos en sus respectivas entidades.

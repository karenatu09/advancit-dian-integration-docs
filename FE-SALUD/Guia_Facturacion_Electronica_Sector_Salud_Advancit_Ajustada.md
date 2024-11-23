
# Manual de Desarrollo para Consumo de Webservice

## 1. **Introducción**
Este documento técnico describe cómo los desarrolladores deben consumir el Web Service de facturación electrónica, 
el cual permite enviar documentos a la DIAN para su validación previa, mediante el método `send_document`. 
La comunicación con el servicio se realiza mediante una petición SOAP que incluye información en formato JSON encriptado en base64.

### **Requisitos previos**
- **URL del WSDL**: 
  - **Pruebas**: Permite realizar pruebas infinitas sin repercusión. URL: `http://pruebas.url.wsdl`
  - **Producción**: URL para operaciones reales: `http://produccion.url.wsdl`
- Implementar la seguridad requerida, como certificados digitales si aplica.
- Uso de la librería SOAP en PHP (u otro lenguaje que soporte SOAP).

## 5. **Relación entre las Cabeceras del XML y los Datos JSON**

El cuerpo de la petición SOAP incluye un bloque `<sendoc>` que contiene varios ítems donde cada uno tiene una clave (`key`) 
en el XML y un valor (`value`) que corresponde a un conjunto de datos JSON codificado en BASE64. 
A continuación, se describe la relación entre los nombres de las cabeceras XML y los datos JSON:

| **Nombre en XML** | **Nombre en JSON** | **Descripción**                                      |
|-------------------|--------------------|------------------------------------------------------|
| `secado`          | `CABDOC`           | Información de la cabecera del documento (factura)   |
| `secldo`          | `CLIDOC`           | Información del cliente                              |
| `sededo`          | `DETDOC`           | Detalle de los productos o ítems del documento       |
| `sedepr`          | `DETALLEPRO`       | Detalle del producto adicional                       |
| `sedeim`          | `DETIMPDOC`        | Detalle de los impuestos aplicados                   |
| `seaddo`          | `ADIDOC`           | Información adicional del documento                  |
| `sedaws`          | `DATOEMP`          | Datos de la empresa que emite el documento           |
|                   | `DATSAL`           | Información adicional relacionada con los ítems      |
|                   | `PURSAL`           | Datos relacionados con archivos                     |
|                   | `PUESAL`           | Datos relacionados con archivos adicionales          |

### **Escenarios de Envío**
Existen 4 tipos de envíos que determinan los campos obligatorios dependiendo del tipo de operación. Los escenarios son:

1. **SS Recaudo**: Archivo `SSCUFE_PN_Comentado`.
2. **SS-SinAporte**: Archivo `IPSA ERP_Comentado`.
3. **Acreditación**: Archivo `SSCUFE_IPS A EPS_Comentado`.
4. **No Acreditación**: Archivo `SS-Reporte_SIN RECAU_Comentado`.

Los archivos están disponibles en el directorio del repositorio.

---

El resto del contenido del documento se mantiene con los ajustes previos relacionados con tablas, ejemplos JSON, 
e instrucciones de codificación en Base64. Por favor, revise las secciones específicas para detalles adicionales.

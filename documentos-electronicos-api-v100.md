# Documentos Electrónicos v1.0.0

### Documento de Especificación Técnica de Integración

## Tabla de Contenidos

- [1. Historial de cambios / Versiones](#-1-historial-de-cambios--versiones)
- [2. General](#-2-general)
- [3. Datos Generales de la Integración](#-3-datos-generales-de-la-integración)
- [4. Datos Generales de las Aplicaciones Backends](#-4-datos-generales-de-las-aplicaciones-backend)
- [5. Datos Generales de las Aplicaciones Cliente](#-5-datos-generales-de-las-aplicaciones-cliente)
- [6. Componentes Predecesores y Relacionados](#-6-componentes-predecesores-y-relacionados)
- [7. Seguridad](#-7-seguridad)
  - [7.1 Tipo de Autenticación](#-71-tipo-de-autenticación)
  - [7.2 Observaciones Adicionales](#-72-observaciones-adicionales)
- [8. Solución Propuesta](#-8-solución-propuesta)
    - [8.1 Requerimientos Funcionales](#-81-requerimientos-funcionales)
        - [8.1.1 Diagrama de Solución](#-811-diagrama-de-solución)
        - [8.1.2 Detalle de las operaciones soportadas](#-812-detalle-de-las-operaciones-soportadas)
            - [8.1.2.1 generarDocumentoElectronicoS4](#-8121-generardocumentoelectronicos4)
            - [8.1.2.2 generarDocumentoElectronicoDEX](#-8122-generardocumentoelectronicodex) 
            - [8.1.2.3 consultarEstadoDocumento](#-8123-consultarestadodocumento)
            - [8.1.2.4 obtenerDocumentoElectronico](#-8124-obtenerdocumentoelectronico)
            - [8.1.2.5 consultarDocumentosPorEstado](#-8125-consultardocumentosporestado)
    - [8.2 Requerimientos no funcionales](#-82-requerimientos-no-funcionales)
        - [8.2.1 Disponibilidad](#-821-disponibilidad)
        - [8.2.2 Transacciones por segundo](#-822-transacciones-por-segundo)
        - [8.2.3 Cantidad de usuarios concurrentes](#-823-cantidad-de-usuarios-concurrentes)
        - [8.2.4 Escalabilidad](#-824-escalabilidad)
- [9. Anexos](#-9-anexos)

## 📚 1. Historial de cambios / Versiones

| Versión | Fecha      | Descripción             | Responsable  |
|---------|------------|-------------------------|--------------|
| v1.0    | 2023-08-04 | Creación del documento. | Jair Paredes |

## 📝 2. General

<table>
    <tbody>
        <tr>
            <td><strong>Objetivo</strong></td>
            <td>Generar y consultar documentos electrónicos de sociedades Alicorp y DEX.</td>
        </tr>
        <tr>
            <td><strong>Alcance</strong></td>
            <td>Generar guías de remisión electrónicas, consultar el estado y el archivo del documento electrónico y consultar documentos electrónicos en base a varios parametros.</td>
        </tr>
        <tr>
            <td><strong>Empresas del Grupo Alicorp</strong></td>
            <td>ALICORP SAA<br />
                ALICORP INVERSIONES S.A.<br />
                MASTERBREAD S.A.<br />
                VITAPRO S.A.<br />
                R TRADING S.A.<br />
                PROORIENTE S.A.<br />
                INTRADEVCO INDUSTRIAL S.A.<br /></td>
        </tr>
        <tr>
            <td><strong>Empresas DEX</strong></td>
            <td>COBERDEX SOCIEDAD ANONIMA CERRADA<br />
                DISTRIBUIDORA CUNZA S.A.<br />
                FUERZADEX S.A.C.<br />
                ATIPANA DEX S.A.C.<br />
                D.L.F. MEDINA RIVERA S.A.<br />
                DISTRIBUIDORA NUGENT S.A<br />
                DISTRIBUCIONES EXCLUSIVAS DEL SUR SOCIEDAD ANONIMA CERRADA<br />
                DISTRIBUIDORA ALIMENTOS DEL VALLE S.A.C.<br />
                DISTRIBUIDORA DE PRODUCTOS DE CONSUMO MASIVO SOCIEDAD ANONIMA CERRADA<br />
                ROSET DISTRIBUCIONES EMPRESA INDIVIDUAL DE RESPONSABILIDAD LIMITADA - ROSET DISTRIBUCIONES E.I.R.L<br />
                DISTRIBUIDORA MADEX SOCIEDAD ANONIMA CERRADA<br />
                VITALE DEX S.A.C.<br />
                MBA DEX SOCIEDAD ANONIMA CERRADA<br />
                DISTRIBUIDORA JC SAC<br />
                DISTRIBUIDORA CASTILLO CASTILLO S.A.C.<br />
                DALIMNORT S.A.C.<br />
                DISTRIBUIDORA MKM S.A.C<br />
                DISTRIBUIDORA AURELIO S.A.C.<br />
                MT DISTRIBUCIONES S.A.C.<br />
                DISTRIBUIDORA OTOYA S.A.C.<br />
                DISTRIBUIDORA ATIX S.A.C.<br />
                DISTRIBUIDORA RODRIGUEZ S.A.<br />
                JM GENG DISTRIBUCIONES S.A.C.<br />
                F&B SUR S.A.C.<br />
                DALIDELO E.I.R.L.<br />
                DIXIAL S.A.C.<br />
                DEX MINALI SOCIEDAD ANONIMA CERRADA<br />
                DISTRIBUCIONES DEL NORTE ORIENTE SOCIEDAD ANONIMA CERRADA<br />
                DISTRIBUIDORA COMERCIAL LUIS ARTURO & XIMENA E.I.R.L.<br />
                ALMA DISTRIBUCIONES E.I.R.L.<br />
                DISTRIBUIDORA A Y D S.A.C.<br />
                DISTRIBUIDORA LOS ALCAPARROS SOCIEDAD ANONIMA CERRADA<br />
                JLJ DISTRIBUCIONES SOCIEDAD ANONIMA CERRADA<br />
                DISTRIBUIDORA BENAVENTE S.A.<br />
                DEX MAYALI SOCIEDAD ANONIMA CERRADA<br />
                MED DISTRIBUCIONES E.I.R.L<br />
            </td>
        </tr>
        <tr>
            <td><strong>Línea de Negocio</strong></td>
            <td>B2B y CMP</td>
        </tr>
        <tr>
            <td><strong>Pais</strong></td>
            <td>Perú</td>
        </tr>
        <tr>
            <td><strong>Proceso de Negocio</strong></td>
            <td>
                - G. de Pedido de Venta Canal Tradicional - GL1 <br/>
                - Programación con Optimizador de Transporte Local - Stand Alone <br/>
                - G. de Despacho con optimizador de transporte - Stand Alone <br/>
                - G. de Pedido de Venta de Canal Moderno <br/>
                - Devolución por Rechazo <br/>
                - G. de Pedido de Exportación <br/>
                - G. de órdenes de transp. y prog. de transp. de exp. LE-TRA <br/>
                - G. de Despacho de Exportación
            </td>
        </tr>
    </tbody>
</table>

## ⚖ 3. Datos Generales de la Integración

<table>
    <tbody>
        <tr>
            <td><strong>Nombre de componente</strong></td>
            <td>Documentos Electrónicos</td>
        </tr>
        <tr>
            <td><strong>Funcionalidades (Operaciones)</strong></td>
            <td>
                - Emisión de documento electrónico DEX<br/>
                - Emisión de documento electrónico S4H<br/>
                - Permite obtener un documento electrónico (PDF, PDF BASE64, XML).<br/>
                - Consulta estado de un documento.<br/>
                - Consulta masiva de documentos por rango de fechas.
            </td>
        </tr>
        <tr>
            <td><strong>Tipo</strong></td>
            <td>
                <input type="checkbox" checked disabled/> API<br/>
                <input type="checkbox" disabled/>  Flujos Programados - Dags<br/>
            </td>
        </tr>
        <tr>
            <td><strong>Protocolo</strong></td>
            <td>HTTPS/REST</td>
        </tr>
        <tr>
            <td><strong>URL Expuesta</strong></td>
            <td>https://apimgw.prd.api-alicorp.com/alicorp/documentos-electronicos/v1/</td>
        </tr>
        <tr>
            <td><strong>Aplicaciones Backend</strong></td>
            <td>
                - SOVOS
            </td>
        </tr>
        <tr>
            <td><strong>Aplicaciones Cliente</strong></td>
            <td>
                - SIDEX<br/>
                - SAP S/4 HANA<br/>
                - Portal Web Corporativo
            </td>
        </tr>
    </tbody>
</table>

## 🗄 4. Datos Generales de las Aplicaciones Backend

| Nombre del Backend | Url / Servicio                                              | Protocolo | Tipo de Autenticación | Usuario de Autenticación |
|:-------------------|:------------------------------------------------------------|:---------:|-----------------------|--------------------------|
| *SOVOS*            | https://ereceipt-pe-alicorp.sovos.com/axis2/services/Online |   http    | Basic                 | adminppl                 |

## 🗄 5. Datos Generales de las Aplicaciones Cliente

| Nombre de la Aplicación del Cliente | IP o Segmento                             | Protocolo  | Tipo de Autenticación | Suscripción                    |
|:------------------------------------|:------------------------------------------|:----------:|-----------------------|--------------------------------|
| *SIDEX*                             | dexapp1 - 10.72.2.212 - ABAP<br/>dexapp2 - 10.72.2.218 - JAVA<br/>dexapp3 - 10.72.2.213 - ABAP<br/>dexapp4 - 10.72.2.219 - JAVA<br/>dexapp5 - 10.72.2.225 - JAVA<br/>dexapp6 - 10.72.2.217 - ABAP          | https/rest | Subscription-Key      | App-Sidex                      |
| *SAP S/4 HANA*                      | 10.76.10.4                                | https/rest | Subscription-Key      | App-S4Hana                     |
| *Portal Web Corporativo*            | https://alieus2appprd01.azurewebsites.net | https/rest | Subscription-Key      | Web-Int-PortalCorporativo-Back |

## 🔗 6. Componentes Predecesores y Relacionados

- N/A.

## 🔒 7. Seguridad

### 🔑 7.1 Tipo de Autenticación

- Subscription-key

### 🔍 7.2 Observaciones Adicionales

- Ninguna.

## 🏋🏻 8. Solución Propuesta

### 📗 8.1 Requerimientos Funcionales

Se implementará una API con un conjunto de operaciones para generar guías de remisión electrónicas, consultar el estado
y el archivo del documento electrónico y consultar documentos electrónicos en base a varios parametros.

### 📈 8.1.1 Diagrama de Solución

![Diagrama de componentes](/flowchart/documentos-electronicos-dc.png)

### 📝 8.1.2 Detalle de las operaciones soportadas

### 📋 Lista de operaciones

| ID                             | Método | PATH                           | Descripción                                                                                                                                       | Destino |
|--------------------------------|--------|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| generarDocumentoElectronicoS4  | POST   | /S4/emision                    | Permite la generación de documentos electrónicos de las S4 con la entidad recaudadora correspondiente.                                            | SOVOS   |
| generarDocumentoElectronicoDEX | POST   | /DEX/emision                   | Permite la generación de documentos electrónicos de las DEX con la entidad recaudadora correspondiente.                                           | SOVOS   |
| consultarEstadoDocumento       | GET    | /estado                        | Permite consultar el estado de un documento electrónico .                                                                                         | SOVOS   |
| obtenerDocumentoElectronico    | GET    | /documento/{numeroCorrelativo} | Permite obtener un documento electrónico (PDF, PDFBASE64,XML).                                                                                    | SOVOS   |
| consultarDocumentosPorEstado   | GET    | /documentos                    | Retorna información de los datos principales de los documentos para un estado determinado para un RUC receptor particular para un rango de fecha. | SOVOS   |                    

### 📌 8.1.2.1 generarDocumentoElectronicoS4

* Diagrama de Secuencia

![Diagrama de secuencia_generar_documento_s4h](/flowchart/documentos-electronicos-ds-generar-documento-s4h.png)

* Mapeo de Campos

| Seq | Proceso                                  | API                                                                             | Dirección | Backend                                                                     |
|:----|:-----------------------------------------|:--------------------------------------------------------------------------------|:---------:|:----------------------------------------------------------------------------|
| 1   | Invoca Redis. getEquivalence             | -                                                                               |  &larr;   | Redis.Equivalences. motivoTraslado                                          |
|     |                                          | API.item.documentoElectronico. tipoDocumento-DFKKBPTAXNUM-TAXTYPE               |  &larr;   | Redis.Equivalences. tipoDocumento                                           |
|     |                                          | API.item.documentoElectronico. remitente. tipoDocumento-DFKKBPTAXNUM-TAXTYPE    |  &larr;   | Redis.Equivalences. tipoDocumentoRemitente                                  |
|     |                                          | API.item.documentoElectronico. destinatario. tipoDocumento-DFKKBPTAXNUM-TAXTYPE |  &larr;   | Redis.Equivalences. tipoDocumentoDestinatario                               |
|     |                                          | API.item.entrega. transportista. tipoDocumento-DFKKBPTAXNUM-TAXTYPE             |  &larr;   | Redis.Equivalences. tipoDocumentoTransportista                              |
|     |                                          | API.item.entrega. carga. unidadMedidaPesoBruto-LIKP-GEWEI                       |  &larr;   | Redis.Equivalences. unidadMedidaPesoBruto                                   |
|     |                                          | API.item.pedido. exportacion. codigoPuertoAeropuerto-ADRC-POST_CODE1            |  &larr;   | Redis.Equivalences. codigoPuertoAeropuerto                                  |
|     |                                          | API.item. item.unidadMedida-LIPS-VRKME                                          |  &larr;   | Redis.Equivalences. unidadMedidaItem                                        |
| 2   | Lee Redis. getTariffItems                | -                                                                               |  &larr;   | Redis.Equivalences. tariff_item                                             |
| 3   | Lee cia_mapping. tariff_item             | Redis.tariffItems                                                               |  &larr;   | ODL.cia_mapping. tariff_item                                                |
| 4   | Lee cia_mapping. eq_electronic_documents | Redis.equivalences                                                              |  &larr;   | ODL.cia_mapping. eq_electronic_documents                                    |
| 5   | Arma request a Sovos                     | SovosWSRequest.ruc                                                              |  &larr;   | API.{body}.documentoElectronico. remitente. numeroDocumento-BUT000-BU_SORT2 |
|     |                                          | SovosWSRequest.docTxt                                                           |  &larr;   | (Trama personalizada)                                                       |
|     |                                          | SovosWSRequest.tipoFoliacion                                                    |  &larr;   | "2"                                                                         |
|     |                                          | SovosWSRequest.tipoRetorno                                                      |  &larr;   | "0"                                                                         |
| 6   | Arma response                            | API.code                                                                        |  &larr;   | SovosWSResponse.Codigo                                                      |
|     |                                          | API.message                                                                     |  &larr;   | SovosWSResponse.Mensaje                                                     |
|     |                                          | API.docId                                                                       |  &larr;   | SovosWSResponse.DocId                                                       |
|     |                                          | API.trama                                                                       |  &larr;   | "Trama Personalizada"                                                       |
|     |                                          | API.notes                                                                       |  &larr;   | SovosWSResponse.Nota                                                        |


:::info NOTA

- Ver anexo [generarDocumentoElectronicoS4 - Mapeo](#-9-anexos).

:::

* Catálogo de Errores

|   #   | Escenario                           | Status Code |                                            Error Message                                            | Descripción |
|:-----:|:------------------------------------|:-----------:|:---------------------------------------------------------------------------------------------------:|:-----------:|
| **1** | Body inválido (no se pudo parsear). |     400     |              Request is not well-formed, syntactically incorrect, or violates schema.               |      -      |
| **2** | Body con algún campo incorrecto.    |     422     | The requested action could not be performed, semantically incorrect, or failed business validation. |      -      |
| **3** | Error interno del servidor.         |     500     |                               An internal server error has occurred.                                |      -      |
| **4** | Error interno del servidor Sovos.   |     500     |                               An internal server error has occurred.                                |      -      |
### 📌 8.1.2.2 generarDocumentoElectronicoDEX

* Diagrama de Secuencia

![Diagrama de secuencia_generar_documento_dex](/flowchart/documentos-electronicos-ds-generar-documento-dex.png)

* Mapeo de Campos

| Seq | Proceso                                  | API                                                                | Dirección | Backend                                                    |
|:----|:-----------------------------------------|:-------------------------------------------------------------------|:---------:|:-----------------------------------------------------------|
| 1   | Invoca Redis. getEquivalence             | API.item. Entrega.MotivoTraslado                                   |  &larr;   | Redis.Equivalences. MotivoTraslado                         |
|     |                                          | API.item. DocumentoElectronico.TipoDocumento                       |  &larr;   | Redis.Equivalences. TipoDocumento                          |
|     |                                          | API.item. Entrega. Carga.UnidadMedidaPesoBruto                     |  &larr;   | Redis.Equivalences. UnidadMedidaPesoBruto                  |
|     |                                          | API.item. DocumentoElectronico. DocumentoRelacionado.TipoDocumento |  &larr;   | Redis.Equivalences. TipoDocumento                          |
|     |                                          | API.item. item.UnidadMedida                                        |  &larr;   | Redis.Equivalences. UnidadMedida                           |
| 2   | Lee cia_mapping. eq_electronic_documents | Redis.Equivalences                                                 |  &larr;   | ODL.cia_mapping. eq_electronic_documents                   |
| 3   | Arma request a Sovos                     | SovosWSRequest.ruc                                                 |  &larr;   | API.{body}.documentoElectronico. remitente.numeroDocumento |
|     |                                          | SovosWSRequest.docTxt                                              |  &larr;   | (Trama personalizada)                                      |
|     |                                          | SovosWSRequest.tipoFoliacion                                       |  &larr;   | "2"                                                        |
|     |                                          | SovosWSRequest.tipoRetorno                                         |  &larr;   | API.{body}.tipoRespuesta                                   |
| 4   | Arma response                            | API.code                                                           |  &larr;   | SovosWSResponse.Codigo                                     |
|     |                                          | API.message                                                        |  &larr;   | SovosWSResponse.Mensaje                                    |
|     |                                          | API.docId                                                          |  &larr;   | SovosWSResponse.DocId                                      |
|     |                                          | API.trama                                                          |  &larr;   | "Trama Personalizada"                                      |
|     |                                          | API.notes                                                          |  &larr;   | SovosWSResponse.Nota                                       |


:::info NOTA

- Ver anexo [generarDocumentoElectronicoDEX - Mapeo](#-9-anexos).

:::

* Catálogo de Errores

|   #   | Escenario                           | Código de Estado | Mensaje de Error                                                                                    | Descripción |
|:-----:|:------------------------------------|:----------------:|:----------------------------------------------------------------------------------------------------|:-----------:|
| **1** | Body inválido (no se pudo parsear). |       400        | Request is not well-formed, syntactically incorrect, or violates schema.                            |      -      |
| **2** | Body con algún campo incorrecto.    |       422        | The requested action could not be performed, semantically incorrect, or failed business validation. |      -      |
| **3** | Error interno del servidor.         |       500        | An internal server error has occurred.                                                              |      -      |
| **4** | Error interno del servidor Sovos.   |       500        | An internal server error has occurred.                                                              |      -      |

### 📌 8.1.2.3 consultarEstadoDocumento

* Diagrama de Secuencia

![Diagrama de secuencia_consulta_estado](/flowchart/documentos-electronicos-ds-consulta-estado.png)

* Mapeo de Campos

| Seq | Description          | API                        | Dirección | Backend                       |
|:----|:---------------------|:---------------------------|:---------:|:------------------------------|
| 1   | Arma request a Sovos | SovosWSRequest.ruc         |  &larr;   | API.{query}.numeroNIF         |
|     |                      | SovosWSRequest.tipoDoc     |  &larr;   | API.{query}.tipoNIF           |
|     |                      | SovosWSRequest.folio       |  &larr;   | API.{query}.numeroCorrelativo |
|     |                      | SovosWSRequest.tipoRetorno |  &larr;   | "3"                           |
| 2   | Arma response        | API.code                   |  &larr;   | SovosWSResponse.Codigo        |
|     |                      | API.message                |  &larr;   | SovosWSResponse.Mensaje       |
|     |                      | API.notes                  |  &larr;   | SovosWSResponse.Nota          |
|     |                      | API.docId                  |  &larr;   | SovosWSResponse.DocId         |

* Catálogo de Errores

|   #   | Escenario                             | Código de Estado | Mensaje de Error                                                                                    | Descripción |
|:-----:|:--------------------------------------|:----------------:|:----------------------------------------------------------------------------------------------------|:-----------:|
| **1** | Body inválido (no se pudo parsear).   |       400        | Request is not well-formed, syntactically incorrect, or violates schema.                            |      -      |
| **2** | Application-Code no debe estar vácio. |       422        | The requested action could not be performed, semantically incorrect, or failed business validation. |      -      |
| **3** | Error interno del servidor.           |       500        | An internal server error has occurred.                                                              |      -      |
| **4** | Error interno del servidor Sovos.     |       500        | An internal server error has occurred.                                                              |      -      |

### 📌 8.1.2.4 obtenerDocumentoElectronico

* Diagrama de Secuencia

![Diagrama de secuencia_obtener_documento](/flowchart/documentos-electronicos-ds-obtener-documento.png)

* Mapeo de Campos

| Seq | Description          | API                        | Dirección | Backend                       |
|:----|:---------------------|:---------------------------|:---------:|:------------------------------|
| 1   | Arma request a Sovos | SovosWSRequest.ruc         |  &larr;   | API.{query}.numeroNIF         |
|     |                      | SovosWSRequest.tipoDoc     |  &larr;   | API.{query}.tipoNIF           |
|     |                      | SovosWSRequest.folio       |  &larr;   | API.{param}.numeroCorrelativo |
|     |                      | SovosWSRequest.tipoRetorno |  &larr;   | API.{query}.tipoDocumento     |
| 2   | Arma response        | API.code                   |  &larr;   | SovosWSResponse.Codigo        |
|     |                      | API.message                |  &larr;   | SovosWSResponse.Mensaje       |
|     |                      | API.notes                  |  &larr;   | SovosWSResponse.Nota          |
|     |                      | API.docId                  |  &larr;   | SovosWSResponse.DocId         |

* Catálogo de Errores

|   #   | Escenario                             | Código de Estado | Mensaje de Error                                                                                    | Descripción |
|:-----:|:--------------------------------------|:----------------:|:----------------------------------------------------------------------------------------------------|:-----------:|
| **1** | Body inválido (no se pudo parsear).   |       400        | Request is not well-formed, syntactically incorrect, or violates schema.                            |      -      |
| **2** | Application-Code no debe estar vácio. |       422        | The requested action could not be performed, semantically incorrect, or failed business validation. |      -      |
| **3** | Error interno del servidor.           |       500        | An internal server error has occurred.                                                              |      -      |
| **4** | Error interno del servidor Sovos.     |       500        | An internal server error has occurred.                                                              |      -      |

### 📌 8.1.2.5 consultarDocumentosPorEstado

* Diagrama de Secuencia

![Diagrama de secuencia_consulta_masiva](/flowchart/documentos-electronicos-ds-consulta-masiva.png)

* Mapeo de Campos

| Seq | Description          | API                        | Dirección | Backend                       |
|:----|:---------------------|:---------------------------|:---------:|:------------------------------|
| 1   | Arma request a Sovos | SovosWSRequest.ruc         |  &larr;   | API.{query}.numeroNIFEmisor   |
|     |                      | SovosWSRequest.rucReceptor |  &larr;   | API.{query}.numeroNIFReceptor |
|     |                      | SovosWSRequest.estado      |  &larr;   | API.{query}.estado            |
|     |                      | SovosWSRequest.fechaInicio |  &larr;   | API.{query}.fechaInicio       |
|     |                      | SovosWSRequest.fechaFin    |  &larr;   | API.{query}.fechaFin          |
| 2   | Arma response        | API.code                   |  &larr;   | SovosWSResponse.Codigo        |
|     |                      | API.message                |  &larr;   | SovosWSResponse.Mensaje       |

* Catálogo de Errores

|   #   | Escenario                             | Código de Estado | Mensaje de Error                                                                                    | Descripción |
|:-----:|:--------------------------------------|:----------------:|:----------------------------------------------------------------------------------------------------|:-----------:|
| **1** | Body inválido (no se pudo parsear).   |       400        | Request is not well-formed, syntactically incorrect, or violates schema.                            |      -      |
| **2** | Application-Code no debe estar vácio. |       422        | The requested action could not be performed, semantically incorrect, or failed business validation. |      -      |
| **3** | Error interno del servidor.           |       500        | An internal server error has occurred.                                                              |      -      |
| **4** | Error interno del servidor Sovos.     |       500        | An internal server error has occurred.                                                              |      -      |

## 📘 8.2 Requerimientos no funcionales

### 📅 8.2.1 Disponibilidad

- [x] Crítico
- [ ] Puede tener tiempo de para

### ⚡ 8.2.2 Transacciones por segundo

- 10 TPS

###  🧑‍💻 8.2.3 Cantidad de usuarios concurrentes

- 40 usuarios

### 🖥 8.2.4 Escalabilidad

- [x] Automático
- [ ] Manual

## 📂 9. Anexos

| ID  | Nombre                                 | Descripción                                                                               | Link                                                                                                                                                                                       |
|:----|:---------------------------------------|:------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | generarDocumentoElectronicoS4 - Mapeo  | Documento con el mapeo de la trama personalizada que se envia a SOVOS desde SAP S/4 HANA. | [Formato SOVOS - Estimación NTTv4.xlsx](https://grupoalicorp.sharepoint.com/:x:/t/ArquitecturaeInnovacion/EYLfaj9-k-1Gt67EZoKkM5QBQh20fDCVgnd7x0WcxEqu4A?e=QPkjIv)                         |
| 2   | generarDocumentoElectronicoDEX - Mapeo | Documento con el mapeo de la trama personalizada que se envia a SOVOS desde SIDEX.        | [PPLPERU_FormatoIntercambio_GRE_3.0_V3_Rev.xlsx](https://grupoalicorp.sharepoint.com/:x:/t/ArquitecturaeInnovacion/ESL_knlM1btInONdWeVWzUMB3Mm07HQN5YgD0b6I20yj-w?e=cGg3Ug)                |
| 3   | Especificación del OpenAPI             | Especificación del OpenAPI del API Documentos Electrónicos.                               | [Documentos Electrónicos.openapi.yaml](https://grupoalicorp.sharepoint.com/:u:/t/ArquitecturaeInnovacion/EYFtkg7RlaxDvxTjbvkYHSQBH-Ze18sxlY4yGoESF99iSg?e=gbHLuG)                          |
| 4   | Diagrama Técnico de Conexiones         | Diagrama Técnico de Conexiones a nivel de infraestructura.                                | [Guias de Remision Electronica Fase 1 y 2 - GRM Infra v2.0.pdf](https://grupoalicorp.sharepoint.com/:b:/t/ArquitecturaeInnovacion/EXsLKID0fLZNldU565chlRQB1Ym-Axq-Eeb6XQBIPUt2Kg?e=zQgfBI) |


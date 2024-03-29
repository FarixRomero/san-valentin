# Customer Management v1.1.0

### Documento de Especificación Técnica de Integración

## Tabla de Contenidos

- [📚 1. Historial de cambios / Versiones](#-1-historial-de-cambios--versiones-developer)
- [📝 2. General](#-2-general-architect)
- [⚖ 3. Datos Generales de la Integración](#-3-datos-generales-de-la-integración-developer)
- [🗄 4. Datos Generales de las Aplicaciones Backend](#-4-datos-generales-de-las-aplicaciones-backend-architect)
- [🗄 5. Datos Generales de las Aplicaciones Cliente](#-5-datos-generales-de-las-aplicaciones-cliente-architect)
- [🔗 6. Componentes Predecesores y Relacionados](#-6-componentes-predecesores-y-relacionados-developer)
- [🔒 7. Seguridad](#-7-seguridad-developer)
    - [🔑 7.1 Tipo de Autenticación](#-71-tipo-de-autenticación)
    - [🔍 7.2 Observaciones Adicionales](#-72-observaciones-adicionales)
- [🏋🏻 8. Solución Propuesta](#-8-solución-propuesta)
    - [📗 8.1 Requerimientos Funcionales ](#-81-requerimientos-funcionales-developer)
    - [📈 8.1.1 Diagrama de Solución](#-811-diagrama-de-solución-architect)
    - [📝 8.1.2 Detalle de las operaciones soportadas](#-812-detalle-de-las-operaciones-soportadas-developer)
    - [📋 Lista de operaciones](#-lista-de-operaciones)
    - [📌 8.1.2.1 GetCustomersByFilters](#-8121-getcustomersbyfilters-developer)
    - [📌 8.1.2.2 getCustomerByCode](#-8122-getcustomerbycode-developer)
    - [📌 8.1.2.3 getAddressesByCustomerCode](#-8123-getaddressesbycustomercode-developer)
    - [📌 8.1.2.4 getDeliveryDatesBySocietyBranchAndCustomerCode](#-8124-getdeliverydatesbysocietybranchandcustomercode-developer)
    - [📌 8.1.2.5 getPaymentConditionsByCustomerCode](#-8125-getpaymentconditionsbycustomercode-developer)
    - [📌 8.1.2.6 getCustomerCreditLine](#-8126-getcustomercreditline-developer)
    - [📌 8.1.2.7 getCustomersBySalespersonCode](#-8127-getcustomersbysalespersoncode-developer)
    - [📌 8.1.2.8 getCreditLineBySalesperson](#-8128-getcreditlinebysalesperson-developer)
    - [📌 8.1.2.9 createCustomer](#-8129-createcustomer-developer)
    - [📌 8.1.2.10 validateCustomer](#-81210-validatecustomer-developer)
    - [📌 8.1.2.11 updateCustomer](#-81211-updatecustomer-developer)
- [📘 8.2 Requerimientos no funcionales](#-82-requerimientos-no-funcionales-architect)
    - [📅 8.2.1 Disponibilidad](#-821-disponibilidad)
    - [⚡ 8.2.2 Transacción por segundo](#-822-transacción-por-segundo)
    - [🧑‍💻 8.2.3 Cantidad de usuarios concurrentes](#-823-cantidad-de-usuarios-concurrentes)
    - [🖥 8.2.4 Escalabilidad](#-824-escalabilidad)
- [📂 9. Anexos](#-9-anexos-developer)

## 📚 1. Historial de cambios / Versiones

| Versión | Fecha      | Descripción             | Responsable       |
|---------|------------|-------------------------|-------------------|
| v1.0    | 2023-08-04 | Creación del documento. | José Luis Vásquez |

## 📝 2. General

<table>
    <tbody>
        <tr>
            <td><strong>Objetivo</strong></td>
            <td>Consultar la información base de un cliente DEX, sus direcciones de entrega, condiciones de pago y fechas preferentes de entrega.</td>
        </tr>
        <tr>
            <td><strong>Alcance</strong></td>
            <td>Obtener la información base de un cliente, interlocutores, direcciones y territorios asociados, consultar las direcciones asociadas a los interlocutores de un cliente DEX, consultar las fechas de entrega preferente de un cliente DEX, consultar las condiciones de pago disponibles de un determinado cliente DEX, consultar la información de línea de crédito de uno o más clientes DEX, obtener la inforación de los clientes, interlocutores, direcciones y territorios asociados a un vendedor, obtener el detalle de la línea de crédito de los clientes de un vendedor, registrar clientes de los vendedores de las DEX, validar un cliente DEX en Sunat o en el ERP, actualizar datos de clientes de los vendedores de las DEX.       </td>
        </tr>
        <tr>
            <td><strong>Empresas del Grupo Alicorp</strong></td>
            <td>ALICORP SAA<br />
                </td>
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
            <td><strong>Negocio</strong></td>
            <td>B2B y CMP</td>
        </tr>
        <tr>
            <td><strong>Pais</strong></td>
            <td>Perú</td>
        </tr>
        <tr>
            <td><strong>Proceso de Negocio</strong></td>
            <td></td>
        </tr>
    </tbody>
</table>

## ⚖ 3. Datos Generales de la Integración

<table>
    <tbody>
        <tr>
            <td><strong>Nombre de componente</strong></td>
            <td>---</td>
        </tr>
        <tr>
            <td><strong>Funcionalidades (Operaciones)</strong></td>
            <td>
                - Permite simulación de ordenes de ventas
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
            <td></td>
        </tr>
        <tr>
            <td><strong>Aplicaciones Backend</strong></td>
            <td>
                - SAP S/4 HANA
            </td>
        </tr>
        <tr>
            <td><strong>Aplicaciones Cliente</strong></td>
            <td>
                - Web de Clientes
            </td>
        </tr>
    </tbody>
</table>

## 🗄 4. Datos Generales de las Aplicaciones Backend


| Nombre del Backend | Url / Servicio                                              | Protocolo | Tipo de Autenticación | Usuario de Autenticación |
|:-------------------|:------------------------------------------------------------|:---------:|-----------------------|--------------------------|
| *SAP S/4 HANA*     | FALTA                                                      |   http    | Basic                 | SYS_3012                 |

## 🗄 5. Datos Generales de las Aplicaciones Cliente

| Nombre de la Aplicación del Cliente | IP o Segmento | Protocolo  | Tipo de Autenticación | Suscripción |
|:------------------------------------|:--------------|:----------:|-----------------------|-------------|
| *WEB DE CLIENTES*                        | TBD           | https/rest | Subscription-Key      | App-WebClientes   |

## 🔗 6. Componentes Predecesores y Relacionados

- N/A.

## 🔒 7. Seguridad

### 🔑 7.1 Tipo de Autenticación

- Subscription-key

### 🔍 7.2 Observaciones Adicionales

- Ninguna.

## 🏋🏻 8. Solución Propuesta

### 📗 8.1 Requerimientos Funcionales

Se implementará una API con un conjunto de operaciones para obtener la información base de un cliente,
interlocutores, direcciones y territorios asociados, consultar las direcciones asociadas a los interlocutores de un
cliente DEX, consultar las fechas de entrega preferente de un cliente DEX, consultar las condiciones de pago disponibles
de un determinado cliente DEX, consultar la información de línea de crédito de uno o más clientes DEX, obtener la
inforación de los clientes, interlocutores, direcciones y territorios asociados a un vendedor, obtener el detalle de la
línea de crédito de los clientes de un vendedor, registrar clientes de los vendedores de las DEX, validar un cliente DEX
en Sunat o en el ERP, actualizar datos de clientes de los vendedores de las DEX.

### 📈 8.1.1 Diagrama de Solución

![Diagrama de componentes](../../../static/flowchart/solucionesdigitalesapi/Arquitectura-Arquitectura-Api-Dex-Customers.png)

### 📝 8.1.2 Detalle de las operaciones soportadas

### 📋 Lista de operaciones

| ID                             | Método | PATH                           | Descripción                                                                                            | Destino |
|--------------------------------|--------|--------------------------------|--------------------------------------------------------------------------------------------------------|---------|
| createOrderSimulation              | POST   | /simulacion                    | Permite permite simular la creación de pedidos de los clientes de Alicorp                               | SAP S/4 HANA   |

### 📌 8.1.2.1 Simulate

- Diagrama de Secuencia

```mermaid
<!-- sequenceDiagram
    title GetCustomersByFilters
    Aplicación Cliente ->>+ CIA API MGM: GetCustomersByFilters Request
    CIA API MGM ->>+ CIA Knative MS Coliving: GetCustomersByFilters Request
    CIA Knative MS Coliving ->>+ CIA Odl: getByFilters Request
    CIA Odl ->>- CIA Knative MS Coliving: DATA Response
    CIA Knative MS Coliving ->>- CIA API MGM: GetCustomersByFilters Response
    CIA API MGM -->>- Aplicación Cliente: GetCustomersByFilters Response -->

```

| Seq | Description    | API                                              | Dirección | Backend                                                                  |
|:----|:---------------|:-------------------------------------------------|:---------:|:-------------------------------------------------------------------------|
| 1   | Arma request a | Api.{query}.documentNumber                       |  &rarr;   | OdlRequest.customer.customer.document_number                             |
|     |                | Api.{query}.documentType                         |  &rarr;   | OdlRequest.customer.customer.document_type                               |
|     |                | Api.{query}.customerCodes                        |  &rarr;   | OdlRequest.customer.customer.customer_code                               |
|     |                | Api.{query}.razonSocial                          |  &rarr;   | OdlRequest.customer.customer.business_name                               |
|     |                | Api.{query}.page                                 |  &rarr;   | OdlRequest.page                                                          |
|     |                | Api.{query}.limit                                |  &rarr;   | OdlRequest.limit                                                         |
| 2   | Arma response  | API.customerCode                                 |  &larr;   | OdlResponse.customer.customer.customer_code                              |
|     |                | API.statusCode                                   |  &larr;   | OdlResponse.customer.customer.status_code                                |
|     |                | API.documentNumber                               |  &larr;   | OdlResponse.customer.customer.document_number                            |
|     |                | API.documentType                                 |  &larr;   | OdlResponse.customer.customer.document_type                              |
|     |                | API.documentTypeDescription                      |  &larr;   | OdlResponse.customer.customer.document_type_description                  |
|     |                | API.name                                         |  &larr;   | OdlResponse.customer.customer.name                                       |
|     |                | API.lastName                                     |  &larr;   | OdlResponse.customer.customer.last_name                                  |
|     |                | API.motherLastName                               |  &larr;   | OdlResponse.customer.customer.mother_last_name                           |
|     |                | API.businessName                                 |  &larr;   | OdlResponse.customer.customer.business_name                              |
|     |                | API.contactInformation.phone                     |  &larr;   | OdlResponse.customer.customer.phone_1                                    |
|     |                | API.contactInformation.email                     |  &larr;   | OdlResponse.customer.customer.email                                      |
|     |                | API.contactInformation.mobilePhone               |  &larr;   | OdlResponse.customer.customer.mobile_phone_1                             |
|     |                | API.creditLimitAmount                            |  &larr;   | OdlResponse.customer.customer.credit_limit_amount                        |
|     |                | API.countryCode                                  |  &larr;   | OdlResponse.customer.customer.country_code                               |
|     |                | API.customerGroup.code                           |  &larr;   | OdlResponse.customer.customer.customer_group_code                        |
|     |                | API.customerGroup.description                    |  &larr;   | OdlResponse.customer.master_dex_clientgroup.description                  |
|     |                | API.customerPriceList.code                       |  &larr;   | OdlResponse.customer.customer.customer_price_list_code                   |
|     |                | API.customerPriceList.description                |  &larr;   | OdlResponse.customer.customer.customer_price_list_description            |
|     |                | API.priceGroup.code                              |  &larr;   | OdlResponse.customer.customer.customer_price_group_code                  |
|     |                | API.priceGroup.description                       |  &larr;   | OdlResponse.customer.customer.customer_price_group_description           |
|     |                | API.blockType.code                               |  &larr;   | OdlResponse.customer.customer.block_type_code                            |
|     |                | API.blockType.description                        |  &larr;   | OdlResponse.customer.customer.block_type_description                     |
|     |                | API.customerZone.code                            |  &larr;   | OdlResponse.customer.customer.customer_zone_code                         |
|     |                | API.customerZone.description                     |  &larr;   | OdlResponse.customer.customer.customer_zone_description                  |
|     |                | API.paymentCondition.code                        |  &larr;   | OdlResponse.customer.customer.payment_condition_code                     |
|     |                | API.paymentCondition.description                 |  &larr;   | OdlResponse.customer.customer.payment_condition_description              |
|     |                | API.paymentMethod.code                           |  &larr;   | OdlResponse.customer.customer.payment_method_code                        |
|     |                | API.paymentMethod.description                    |  &larr;   | OdlResponse.customer.customer.payment_method_description                 |
|     |                | API.cluster.code                                 |  &larr;   | OdlResponse.customer.customer_segmentation.cluster_code                  |
|     |                | API.cluster.description                          |  &larr;   | OdlResponse.customer.customer_segmentation.cluster_description           |
|     |                | API.potentialSegment.code                        |  &larr;   | OdlResponse.customer.customer_segmentation.potential_segment_code        |
|     |                | API.potentialSegment.description                 |  &larr;   | OdlResponse.customer.customer_segmentation.potential_segment_description |
|     |                | API.businessSegmentCode                          |  &larr;   | OdlResponse.customer.customer.business_segment_code                      |
|     |                | API.corporateSegmentCode                         |  &larr;   | OdlResponse.customer.customer.corporate_segment_code                     |
|     |                | API.retentionFlag                                |  &larr;   | OdlResponse.customer.customer.retention_flag                             |
|     |                | API.shippingDocumentFlag                         |  &larr;   | OdlResponse.customer.customer.shipping_document_flag                     |
|     |                | API.telephoneSaleFlag                            |  &larr;   | OdlResponse.customer.customer.telephone_sale_flag                        |
|     |                | API.perfectClientFlag                            |  &larr;   | OdlResponse.customer.customer_segmentation.perfect_client_flag           |
|     |                | API.interlocutorCode                             |  &larr;   | OdlResponse.customer.customer.interlocutor_code                          |
|     |                | API.mainAddressCode                              |  &larr;   | OdlResponse.customer.customer.address_code                               |
|     |                | API.interlocutors[].interlocutorCode             |  &larr;   | OdlResponse.customer.interlocutor.interlocutor_code                      |
|     |                | API.interlocutors[].customerCode                 |  &larr;   | OdlResponse.customer.interlocutor.customer_code                          |
|     |                | API.interlocutors[].name                         |  &larr;   | OdlResponse.customer.interlocutor.name                                   |
|     |                | API.interlocutors[].status                       |  &larr;   | OdlResponse.customer.interlocutor.status                                 |
|     |                | API.interlocutors[].addressCode                  |  &larr;   | OdlResponse.customer.interlocutor.address_code                           |
|     |                | API.interlocutors[].branchCode                   |  &larr;   | OdlResponse.customer.interlocutor.branch_code                            |
|     |                | API.interlocutors[].distributorCode              |  &larr;   | OdlResponse.customer.interlocutor.society_code                           |
|     |                | API.interlocutors[].deliveryDays                 |  &larr;   | OdlResponse.customer.interlocutor.delivery_days                          |
|     |                | API.interlocutors[].deliveryPriority             |  &larr;   | OdlResponse.customer.interlocutor.delivery_priority                      |
|     |                | API.interlocutors[].expeditionConditionCode      |  &larr;   | OdlResponse.customer.interlocutor.expedition_condition_code              |
|     |                | API.interlocutors[].posType                      |  &larr;   | OdlResponse.customer.interlocutor.pos_type                               |
|     |                | API.interlocutors[].address.addressCode          |  &larr;   | OdlResponse.customer.address.address_code                                |
|     |                | API.interlocutors[].address.urbanization         |  &larr;   | OdlResponse.customer.address.urbanization                                |
|     |                | API.interlocutors[].address.wayPrefixCode        |  &larr;   | OdlResponse.customer.address.way_prefix_code                             |
|     |                | API.interlocutors[].address.wayPrefixDescription |  &larr;   | OdlResponse.customer.address.way_prefix_description                      |
|     |                | API.interlocutors[].address.way                  |  &larr;   | OdlResponse.customer.address.way                                         |
|     |                | API.interlocutors[].address.addressNumber        |  &larr;   | OdlResponse.customer.address.address_number                              |
|     |                | API.interlocutors[].address.interior             |  &larr;   | OdlResponse.customer.address.interior                                    |
|     |                | API.interlocutors[].address.block                |  &larr;   | OdlResponse.customer.address.block                                       |
|     |                | API.interlocutors[].address.lot                  |  &larr;   | OdlResponse.customer.address.lot                                         |
|     |                | API.interlocutors[].address.kmNumber             |  &larr;   | OdlResponse.customer.address.km_number                                   |
|     |                | API.interlocutors[].address.fullAddress          |  &larr;   | OdlResponse.customer.address.full_address                                |
|     |                | API.interlocutors[].address.addressLongitude     |  &larr;   | OdlResponse.customer.address.address_longitude                           |
|     |                | API.interlocutors[].address.addressLatitude      |  &larr;   | OdlResponse.customer.address.address_latitude                            |
|     |                | API.interlocutors[].address.reference            |  &larr;   | OdlResponse.customer.address.reference_1                                 |
|     |                | API.interlocutors[].address.countryCode          |  &larr;   | OdlResponse.customer.address.country_code                                |
|     |                | API.interlocutors[].address.ubigeoCode           |  &larr;   | OdlResponse.customer.address.ubigeo_code                                 |
|     |                | API.interlocutors[].address.state                |  &larr;   | OdlResponse.customer.address.state                                       |
|     |                | API.interlocutors[].address.province             |  &larr;   | OdlResponse.customer.address.province                                    |
|     |                | API.interlocutors[].address.district             |  &larr;   | OdlResponse.customer.address.district                                    |
|     |                | API.interlocutors[].address.ubigeoType           |  &larr;   | OdlResponse.customer.address.ubigeo_type                                 |
|     |                | API.interlocutors[].address.module               |  &larr;   | OdlResponse.customer.address.module                                      |
|     |                | API.interlocutors[].address.blockCode            |  &larr;   | OdlResponse.customer.address.block_code                                  |
|     |                | API.interlocutors[].address.isPrincipal          |  &larr;   | OdlResponse.isPrincipal                                                  |
|     |                | API.distributorCode                              |  &larr;   | OdlResponse.customer.customer.society_code                               |
|     |                | API.branchCode                                   |  &larr;   | OdlResponse.customer.customer.branch_code                                |
|     |                | API.regimeCode                                   |  &larr;   | OdlResponse.customer.customer.customer_regime_code                       |
|     |                | API.erpCode                                      |  &larr;   | OdlResponse.customer.customer.erp_code                                   |
|     |                | API.erpDescription                               |  &larr;   | OdlResponse.utils.erp.erp_description                                    |
|     |                | API.originCreateDate                             |  &larr;   | OdlResponse.customer.customer.origin_creation_date                       |
|     |                | API.originUpdateDate                             |  &larr;   | OdlResponse.customer.customer.origin_updated_date                        |
|     |                | API.sellers[].name                               |  &larr;   | OdlResponse.distributor.tp_salesforce_assignment.name                    |
|     |                | API.sellers[].email                              |  &larr;   | OdlResponse.distributor.tp_salesforce_assignment.email                   |
|     |                | API.distributorName                              |  &larr;   | OdlResponse.distributor.society.name                                     |
|     |                | API.perceptionAgent                              |  &larr;   | OdlResponse.distributor.society.perception_flag                          |
|     |                | API.territories[].countryCode                    |  &larr;   | OdlResponse.customer.territory.country_code                              |
|     |                | API.territories[].territoryCode                  |  &larr;   | OdlResponse.customer.territory.territory_code                            |
|     |                | API.territories[].dayOfVisit                     |  &larr;   | OdlResponse.customer.territory.day_of_visit                              |
|     |                | API.territories[].periodicity                    |  &larr;   | OdlResponse.customer.territory.periodicity                               |
|     |                | API.territories[].sequence                       |  &larr;   | OdlResponse.customer.territory.sequence                                  |
|     |                | API.territories[].salesforceCode                 |  &larr;   | OdlResponse.distributor.employee_territory.sales_force_code              |
|     |                | API.distributor.entityType                       |  &larr;   | OdlResponse.entityType                                                   |
|     |                | API.distributor.id                               |  &larr;   | OdlResponse.id                                                           |
|     |                | API.distributor.href                             |  &larr;   | OdlResponse.href                                                         |

- Catálogo de Errores

|   #   | Escenario                   | Status Code |                                            Error Message                                            | Descripción |
|:-----:|:----------------------------|:-----------:|:---------------------------------------------------------------------------------------------------:|:-----------:|
| **1** | Algún campo incorrecto.     |     422     | The requested action could not be performed, semantically incorrect, or failed business validation. |      -      |
| **2** | Error interno del servidor. |     500     |                               An internal server error has occurred.                                |      -      |


## 📘 8.2 Requerimientos no funcionales

### 📅 8.2.1 Disponibilidad

- [x] Crítico
- [ ] Puede tener tiempo de para

### ⚡ 8.2.2 Transacción por segundo

- 10 tps

### 🧑‍💻 8.2.3 Cantidad de usuarios concurrentes

- 40 usuarios

### 🖥 8.2.4 Escalabilidad

- [x] Automático
- [ ] Manual

## 📂 9. Anexos

| ID | Nombre                                                     | Descripción                                                | Link                                                                                                                                                                          |
|:---|:-----------------------------------------------------------|:-----------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1  | Arquitectura DS CustomerManagement                         | Diagrama de secuencia interacción.                         | [Arquitectura-DS-CustomerManagement](https://grupoalicorp.sharepoint.com/:b:/t/ArquitecturaeInnovacion/EWPG6WJ-r_9As7VkuyvlSXwB38PN7NIuhZvLgugxHkRmwQ?e=NPFleg)               |
| 2  | Arquitectura - Arquitectura - CustomerManagement           | Diagrama de componentes                                    | [Arquitectura - Arquitectura - CustomerManagement](https://grupoalicorp.sharepoint.com/:i:/t/ArquitecturaeInnovacion/Ebg6u1GlmKNBgHGHpgMKFF8BI0CXPAryTYzWqRjvu33ZgQ?e=PPQTHU) |
| 3  | Documentos de pruebas QA                                   | Evidencias de Pruebas Funcionales.                         | [Documentos de pruebas QA](https://grupoalicorp.sharepoint.com/:w:/t/ArquitecturaeInnovacion/ETNLm8xz4c5Oj6PFQO56-FEBIIVenvp6WqPkoOVLp4Q1Fg?e=y1E7Dz)                         |
| 4  | Diagrama Técnico de Conexiones                             | Diagrama Técnico de Conexiones a nivel de infraestructura. | [Diagrama Técnico de Conexiones](https://grupoalicorp.sharepoint.com/:b:/t/ArquitecturaeInnovacion/EVco2apKoj1Bk2lKRUyvQggBjE2XnW8sqx4T8hNPLzXoIg)                            |
| 5  | Especificación del OpenAPI                                 | Especificación del OpenAPI                                 | [Especificación del OpenAPI](https://grupoalicorp.sharepoint.com/:u:/t/ArquitecturaeInnovacion/EcCI8MqFrqhOmx_dS1RH_dIBbQNXTb7HGf2Vn0UrIUYtDQ?e=Sm7egW)                       |

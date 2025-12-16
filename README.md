# Tuesday Tech Tips - Power Platform Solution

## 📄 Descripción de la Solución
**Tuesday Tech Tips** es una aplicación construida sobre Microsoft Power Platform diseñada para actuar como un inventario centralizado de conocimientos técnicos dentro de L'Oréal.

Su propósito principal es registrar, catalogar y hacer un seguimiento de los "consejos técnicos" que se envían a los empleados. La aplicación resuelve el problema de la pérdida de información histórica, permitiendo consultar qué temas se han tratado en fechas específicas y evitando la repetición o pérdida de conocimientos valiosos compartidos semanalmente.

## 🏗 Arquitectura Técnica
Esta solución es una implementación "Low-Code/No-Code" construida íntegramente en el entorno **L'Oréal – Power Platform**.

### Componentes Principales:
*   **Power Apps (Canvas App):** Interfaz de usuario principal para la entrada, visualización y filtrado de los consejos.
*   **Power Automate (Cloud Flows):** Gestiona la lógica de backend, específicamente la generación de reportes y exportación de datos.
*   **SharePoint & Microsoft Lists:** Actúan como fuente de datos (backend) para almacenar el inventario de consejos y la lista de administradores autorizados.
*   **Excel Online (Business):** Utilizado como plantilla y destino para la exportación de datos.

## ⚙ Flujos de Automatización Clave
El repositorio contiene la lógica para los siguientes procesos críticos, que CodeWiki debe analizar:

### 1. GLOBAL-TT_ExportExcel
Este flujo se activa mediante un botón en la galería principal de la Power App.
*   **Trigger:** Manual (botón de Excel en la app).
*   **Entrada:** Recibe un archivo JSON con la información visible actualmente en la app (respetando los filtros aplicados por el usuario).
*   **Proceso:**
    1.  Procesa el JSON recibido.
    2.  Utiliza una plantilla de Excel predefinida.
    3.  Crea una tabla nueva en un archivo Excel con los datos.
*   **Salida:** Devuelve la ruta (path) del nuevo archivo Excel a la Power App para que el usuario pueda descargarlo o abrirlo automáticamente.

## 🔐 Seguridad y Acceso
*   **Autenticación:** Basada en cuentas corporativas de L'Oréal (SSO).
*   **Autorización:**
    *   **Usuarios Generales:** Requieren que el enlace de la aplicación sea compartido con ellos.
    *   **Administradores:** Para registrar nuevos consejos, el sistema realiza una validación contra una **Lista de SharePoint** de seguridad. Si el usuario no está en esa lista, no podrá acceder a las funciones de administración.

## 💾 Datos y Recuperación
*   **Backup:** Se realizan copias de seguridad diarias almacenadas en SharePoint (ej. EMEA- Employee Experience).
*   **Restauración:** La solución puede ser recuperada importando el archivo ZIP exportado y re-habilitando las conexiones a los orígenes de datos (SharePoint/Outlook/Excel).

## 👥 Propiedad de la Solución (Ownership)
*   **Solution Owner:** Employee Success Department.
*   **Gestores del Proyecto:** Javier Ruidiaz, Matthew Freeth.
*   **Administración de Tips:** Annie Helps.

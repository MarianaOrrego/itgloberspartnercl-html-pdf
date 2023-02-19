# PDF READER


<!-- DOCS-IGNORE:start -->
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-1-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->
<!-- DOCS-IGNORE:end -->

Lector de PDF embebido en la pagina, el cual permite mostrar información relevante de manera comoda. 

![image](https://user-images.githubusercontent.com/83648336/219948437-42670b7d-d2e1-4519-98a1-7e9d103786a4.png)

## Configuración

1. Usar el template [vtex-app](https://github.com/vtex-apps/react-app-template)
2. Modificar el `manifest.json`
     ```json 
        {
          "vendor": "itgloberspartnercl",
          "name": "pdf-reader",
          "version": "0.0.1",
          "title": "Lector de PDF",
          "description": "Lector de PDF que permite mostrar PDFs nativos en VTEX IO",
        }
     ``` 
      **vendor:** nombre del cliente o información suministrada por él

      **name:** nombre del componente

      **version:** versión del componente

      **title:** titulo asigando al componente

      **description:** breve descripción del componente


   Agregar en la sección `builders` dentro del `manifest.json` un `store`

    ```json   
        "store" : "0.x"
    ```
   En `dependencies` para este componente no se requiere nada, por ende, queda vacío 

    ```json   
        "dependencies": {}
    ```  
3. En el template se tienen dos `package.json` en ambos se debe modificar la `version` y el `name` 
   ```json 
        "version": "0.0.1",
        "name": "pdf-reader"
   ```  
4. Agregar a la carpeta raíz una carpeta llamada `store`, dentro crear un file llamado `interfaces.json`, en este file se tendrá la siguiente configuración:
    ```json 
        {
          "pdf-reader": {
            "component": "PdfReader",
            "render": "client"
          }
        }
    ```
      Se especifica el nombre del componente con el cual será llamado en el `store-theme` de la tienda que se esta realizando, dentro se encuentra el `component` (se debe poner el nombre del componente React a realizar) y por ultimo el `render` donde se especifica que su renderización será solo en la parte del *cliente* 

5. Finalizado los puntos anteriores, se procede a ingresar a la carpeta `react` en la cual se realizan las siguientes configuraciones: 
    
    5.1. Ejecutar el comando `yarn install` para preparar las dependencias
    
    5.2. Crear el functional component `PdfReader.tsx` con la siguiente configuración 
    
    ```typescript
          import PdfReader from './components/PdfReader'

          export default PdfReader;
    ```   
    5.3. Crear una carpeta llamada `components`, dentro se tiene el functional component `PdfReader` con la configuración necesaria para el funcionamiento del componente, se tienen las importaciones empleadas y el desarrollo delc componente
    ```typescript
          import React, { useEffect, useState } from 'react'

          type Props = {
              pdfUrl: string,
              width: number,
              height: number
          }

          const PdfReader = ({ pdfUrl, width, height }: Props) => {

              const [mounted, setMounted] = useState(false)

              useEffect(() => {
                  setMounted(true)
              }, [])

              return (
                  mounted && (
                      <div className='flex justify-center'>
                          <object
                              data={pdfUrl}
                              type="aplication/pdf"
                              width={width}
                              height={height}
                          >
                              <iframe
                                  title="PDF"
                                  src={pdfUrl}
                                  width={width}
                                  height={height}
                              >
                                  <p>Este navegador no soporta PDF</p>
                              </iframe>
                          </object>
                      </div>
                  )
              )
          }

          export default PdfReader
    ```

6. Linkear el componente custom al `store-theme` de la tienda base

    6.1. Iniciar sesión 
    ```console
       vtex login <vendor>
    ```

    6.2. Elegir el `workspace` en el cual se esta trabajando
    ```console
       vtex use <nombre_worksapce>
    ```

    6.3. Linkear el componente
    ```console
       vtex link
    ```

    6.4. Verificar que el componente quede linkeado, para eso se emplea el siguiente comando

     ```console
        vtex ls
     ```

    En consola debe verse las aplicaciones linkeadas al proyecto, verificando de esta forma que el componente quedo listo para emplearse:

    ```console
        Linked Apps in <vendor> at workspace <nombre_store_theme>
        itgloberspartnercl.pdf-reader                   0.0.1
     ```
      
7. Hacer el llamado del componente desde el `store theme`

## Propiedades

### `Props` 

| Nombre Prop  | Tipo           | Descripción    |
| ------------ | ---------------| -----------------------------------------------------------------------------------------------------------------------------------|
| `pdfUrl`     | `string`       | Propiedad a la cual se le pasará la URL del PDF a mostrar desde el `store theme` | 
| `width`      | `number`       | Propiedad que hace referencia al ancho que tendrá el lector del PDF, se da la propiedad desde el `store theme` | 
| `height`     | `number`       | Propiedad que hace referencia al alto que tendrá el lector del PDF, se da la propiedad desde el `store theme` | 

Tipos de Prop empleadas: 

- `string`  
- `number` 

<!-- DOCS-IGNORE:start -->

## Colaboradores ✨

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

Mariana Orrego Franco

<!-- DOCS-IGNORE:end -->

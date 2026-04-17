# Cliente de servicio MCP modo STDIO

Servicio MCP (Model Context Protocol) que proporciona una API para consultar una base de datos de libros a través del protocolo STDIO.

## Descripción del Servicio

Este servicio MCP implementa las siguientes herramientas:
- **get-book-by-title**: Obtiene información básica de un libro por título
- **get-book-by-isbn**: Obtiene información detallada de un libro por ISBN
- **get-books-by-titles**: Obtiene información de múltiples libros por títulos
- **get-books-by-isbn-list**: Obtiene información detallada de múltiples libros por ISBNs

## Requisitos Previos

- **Node.js**: v18 o superior
- **npm**: v9 o superior

## Pasos para Levantar el Servicio MCP en un Nuevo Proyecto

### 1. Clonar o Copiar el Proyecto

```bash
git clone <repositorio> tu-proyecto
cd tu-proyecto
```

### 2. Instalar Dependencias

```bash
npm install
```

Las dependencias necesarias son:
- `@modelcontextprotocol/sdk`: SDK oficial del Model Context Protocol
- `zod`: Librería para validación de esquemas

### 3. Crear el Archivo de Configuración MCP (mcp.json)

En la raíz del proyecto, o en la carpeta `.vscode/`, crea un archivo llamado `mcp.json`:

#### Ubicación: `.vscode/mcp.json`

```json
{
  "mcpServers": {
    "book-database": {
      "command": "node",
      "args": ["build/index.js"],
      "cwd": "${workspaceFolder}"
    }
  }
}
```

**Explicación de los campos:**
- `mcpServers`: Objeto que contiene la configuración de todos los servidores MCP
- `"book-database"`: Nombre identificador del servidor (puede personalizarse)
- `command`: Comando para ejecutar el servidor (en este caso, Node.js)
- `args`: Argumentos para el comando (ruta al archivo compilado)
- `cwd`: Directorio de trabajo (${workspaceFolder} apunta a la raíz del proyecto)

### 4. Compilar el Código TypeScript (si aplica)

Si el proyecto incluye código TypeScript en la carpeta `src/`, compílalo:

```bash
npm run build
```

### 5. Iniciar el Servidor MCP

```bash
npm start
```

O manualmente:

```bash
node build/index.js
```

El servidor debería mostrar en la consola:
```
Book database MCP Server running on stdio
```

### 6. Verificar que el Servidor Está Activo

El servidor se comunica a través de STDIO (entrada/salida estándar) con VS Code o el cliente MCP.

## Estructura del Proyecto

```
.
├── .vscode/
│   └── mcp.json                 # Configuración MCP
├── build/
│   ├── index.js                 # Archivo compilado del servidor
│   └── data/
│       ├── books.json           # Base de datos de libros (información básica)
│       └── books-details.json   # Base de datos de libros (información detallada)
├── package.json                 # Dependencias y scripts de Node.js
└── README.md                    # Documentación
```

## Integración con VS Code

Una vez configurado el archivo `.vscode/mcp.json`, VS Code reconocerá automáticamente el servidor MCP y podrás usar sus herramientas a través de:
- GitHub Copilot Chat
- Extensiones que soporten MCP
- APIs de cliente MCP

## Ejemplo de Uso

Para buscar un libro por título usando la herramienta `get-book-by-title`:

```
Entrada: title = "The Hobbit"
Salida:
  ISBN: 0547928227
  title: The Hobbit
  author: J.R.R. Tolkien
```

## Campos de Datos

### books.json
- `ISBN`: Identificador único del libro
- `title`: Título del libro
- `author`: Autor del libro

### books-details.json
- `ISBN`: Identificador único del libro
- `summary`: Resumen o sinopsis del libro
- `date`: Fecha de publicación
- `author`: Autor del libro

## Solución de Problemas

### Error: "Cannot find package '@modelcontextprotocol/sdk'"
**Solución:** Ejecuta `npm install` para instalar todas las dependencias.

### Error: "Cannot find module './data/books.json'"
**Solución:** Verifica que los archivos de datos existan en `build/data/`.

### Servidor no inicia
**Solución:** Asegúrate de:
1. Tener Node.js instalado correctamente
2. Haber ejecutado `npm install`
3. El archivo `build/index.js` existe y es válido

## Licencia

Este proyecto está bajo licencia MIT.
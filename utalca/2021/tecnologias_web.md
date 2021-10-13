# Tecnologías Web

## Tabla de Contenidos

1. [Semana 1](#semana-1)
2. [Semana 2](#semana-2)

## Semana 1

### Setup de codeignater:
  - Descargar codeignater v3
  - Descomprimir
  - Crear una carpeta de proyecto en la siguiente ruta: `/opt/lampp/htdocs`
  - Copiar el contenido de codeignater en la carpeta del proyecto
  - Instalar xampp
  - Iniciar Apache Web Server en xampp
  - Abrir en el navegador: `localhost/<nombreCarpetaProyecto>`
  - Cambiar el owner del proyecto: `sudo chown -R <newOwner> <projectFolder>`
  - Modificar el archivo `/etc/php/php.ini` para habilitar la extensión `intl`
  - Correr el servidor con `php spark serve`.
  - Iniciar MySQL database en XAMPP
  - Abrir en el navegador: `localhost/phpmyadmin`



### Estructura del proyecto
  - El controlador principal es `application/controllers/Welcome.php`

#### Archivos de configuración
  - `autoload.php` sirve para cargar librerías, trabajar con sesiones previamente iniciadas, helpers,

  Nosotros vamos a trabajar con el helper de url que se encuentra en `/system/helpers`:

        $autoload['helper'] = array('url');

  A continuación se puede editar `/application/config/config.php`:

        $config['base_url'] = 'http://localhost/primeraclase';

  Luego en `welcome_message.php` se tiene que en el `<head>` agregar:

        <link rel="stylesheet" type="text/css" href="<?php echo base_url() ?> css/style1.css" />


### Actividades
1. Refactorizar estilos

  - En el archivo `welcome_message.php` cortar todo el contenido del tag `style` y moverlo al archivo /css/style1.css
  - Agregar en el `welcome_message.php` un link a la hoja de estilo:

        <link> rel="stylesheet" type="text/css" href="/css/style1.css" </link>

2. Es una buena práctica separar el contenido de las páginas en archivos diferentes

  - Ir al archivo `welcome_message.php`:

      - Cortar desde el inicio hasta el principio del  `<body>` y pegarlo en `/application/views/header.php`
      - Cortar desde el div que cerraba el `<body>` hasta el final y pegarlo en `application/views/footer.php `

  - Crear un archivo `dos.php`

  - Ir al controlador `/application/controllers/Welcome.php` y llamar a las funciones `$load`

```
    public function index()	{
      $this->load->view('header');
      $this->load->view('welcome_message');
      $this->load->view('footer');
	}
```

```
    public function dos()	{
      $this->load->view('header');
      $this->load->view('dos');
      $this->load->view('footer');
	}
```

   - En el navegador ir a la url: `http://localhost/primeraclase/index.php/welcome/dos `




## Semana 2

- Instalar [bootstrap](https://getbootstrap.com/docs/4.5/getting-started/introduction/)
    - en `header.php` agregar las 4 líneas que salen en la sección BootstrapCDN

- Ver [jqueryui](jqueryui.com)



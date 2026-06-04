# SIGTH-Z8 · Sistema de Gestión del Parte Policial · Talento Humano Zona 8

Sistema web para el registro, modificación por dependencias, validación diaria y
monitoreo en tiempo real del **Parte Policial** de la Policía Nacional del Ecuador
(Zona 8: Guayas · Santa Elena · Galápagos).

## Características

- **Visualizador de Parte General**: KPIs, gráficas (Chart.js), filtros por dependencia/estado/grupo, búsqueda, paginación, guardado del día, impresión con responsable y exportación a PDF.
- **Ingreso por Dependencias**: tarjetas dinámicas — **verde** = validada hoy, **rojo** = pendiente. Edición de `Función`, `Novedades/Alertas`, `Grupo` y `Estado`; guardado por unidad y **exportación a PDF de la unidad validada**.
- **Persistencia por fecha**: cada día se respalda como snapshot independiente en el navegador (`localStorage`), conservando los datos base intactos.
- **Diseño**: Glassmorphism institucional, azul `#001b4a` y oro `#d4af37`, Bootstrap 5, Bootstrap Icons, SweetAlert2.

## Estructura del proyecto

```
sigth-z8/
├── index.html              # Menú principal (Parte Policial DMG)
├── visualizador.html       # Opción 1 · Visualizador Parte General
├── dependencias.html       # Opción 2 · Ingreso por Dependencias
├── assets/
│   ├── styles.css          # Estilos glassmorphism
│   ├── data.js             # Capa de datos (carga JSON + persistencia por fecha)
│   ├── visualizador.js     # Lógica opción 1
│   └── dependencias.js     # Lógica opción 2
├── data/
│   └── personal.json       # ← DATOS (separados del código)
├── tools/
│   └── csv_to_json.py      # Regenera personal.json desde un CSV
├── .gitignore              # Protege el CSV crudo (no se sube al repo)
└── README.md
```

## Protección de datos (separación datos ↔ código)

- El código **no contiene datos personales embebidos**. Los registros viven solo en `data/personal.json`.
- El CSV original (`datos.csv` / `base.csv`) está **ignorado por Git** (`.gitignore`) y nunca se sube al repositorio.
- Para actualizar la base sin tocar el código:
  ```bash
  python tools/csv_to_json.py base.csv
  ```
  Esto regenera `data/personal.json`. Reemplazar solo ese archivo actualiza todo el sistema.

> Nota de privacidad: `data/personal.json` contiene datos personales (cédula, celular).
> Si el repositorio es **público**, considera mantener `personal.json` también en `.gitignore`
> y cargarlo por separado en el servidor, o publicar el repo en **privado**.

## Despliegue en GitHub Pages

1. Crear un repositorio y subir el contenido de esta carpeta:
   ```bash
   git init
   git add .
   git commit -m "SIGTH-Z8 inicial"
   git branch -M main
   git remote add origin https://github.com/USUARIO/sigth-z8.git
   git push -u origin main
   ```
2. En GitHub: **Settings → Pages → Source: `main` / root**.
3. Acceder a `https://USUARIO.github.io/sigth-z8/`.

## Uso diario

1. Entrar a **Ingreso Parte dependencias**, validar cada unidad (pasa de roja a verde).
2. En **Visualizador Parte General**, revisar KPIs/gráficas, **Guardar día** e **Imprimir/Exportar PDF** con el nombre del responsable.

## Tecnologías

HTML5 · Bootstrap 5 · Bootstrap Icons · Chart.js · SweetAlert2 · jsPDF + AutoTable · Python (utilidad de conversión).

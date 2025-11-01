# Incrustar Hydra en HTML

Guía paso a paso para incrustar Hydra en una página HTML y usar el canvas como fondo de página.

## Pasos

### 1. Incluir la librería

Incluye el script de Hydra desde el CDN en el `<head>`:

```html
<script src="https://cdn.jsdelivr.net/npm/hydra-synth/dist/hydra-synth.js"></script>
```

### 2. Inicializar Hydra

Crea una instancia de Hydra:

```javascript
var hydra = new Hydra({ detectAudio: false })
```

### 3. Configurar el Canvas como Background

**CSS:**
```css
body {
    margin: 0;
    padding: 0;
    overflow: hidden;
    position: relative;
}

#hydra-canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: -10000;
}
```

`z-index: -10000` coloca el canvas detrás de todo el contenido HTML

**JavaScript:**
```javascript
setTimeout(() => {
    const canvas = document.querySelector('canvas');
    if (canvas) {
        canvas.id = 'hydra-canvas';
    }
}, 100);
```

El `setTimeout` es necesario porque Hydra crea el canvas de forma asíncrona

### 4. Escribir tu Código Hydra

Después de la inicialización, escribe tu código Hydra:

```javascript
// Tu código Hydra aquí
shape(20, 0.1, 0.01)
    .scale(() => Math.sin(time) * 3)
    .out(o0)

render(o0)
```
Asegurate de usar `render()` al final para mostrar el resultado final

## Estructura HTML Completa

```html
<!DOCTYPE html>
<html>
<head>
    <title>Hydra Incrustado</title>
    <script src="https://cdn.jsdelivr.net/npm/hydra-synth/dist/hydra-synth.js"></script>
    <style>
        body {
            margin: 0;
            padding: 0;
            overflow: hidden;
            position: relative;
        }
        
        #hydra-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -10000;
        }
        
        .content {
            color: white;
            text-align: center;
            padding: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
        }
    </style>
</head>
<body>
    <script>
        var hydra = new Hydra({ detectAudio: false })
        
        setTimeout(() => {
            const canvas = document.querySelector('canvas');
            if (canvas) {
                canvas.id = 'hydra-canvas';
            }
        }, 100);
        
        // Tu código Hydra aquí
        shape(20, 0.1, 0.01)
            .scale(() => Math.sin(time) * 3)
            .out(o0)
        
        render(o0)
    </script>
    
    <div class="content">
        <h1>Tu Contenido Aquí</h1>
        <p>El canvas de Hydra está como fondo</p>
    </div>
</body>
</html>
```

## Recursos

- [Editor online de Hydra](https://hydra.ojack.xyz)

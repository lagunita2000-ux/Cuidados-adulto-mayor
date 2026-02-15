<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Aplicación</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            padding: 40px;
            max-width: 600px;
            width: 100%;
        }

        h1 {
            color: #333;
            margin-bottom: 30px;
            text-align: center;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #555;
            font-weight: bold;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            font-family: Arial, sans-serif;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        button {
            width: 100%;
            padding: 12px;
            background: #667eea;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover {
            background: #764ba2;
        }

        .resultado {
            margin-top: 30px;
            padding: 20px;
            background: #f0f4ff;
            border-radius: 8px;
            display: none;
        }

        .resultado.activo {
            display: block;
        }

        .resultado p {
            color: #333;
            line-height: 1.6;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🏥 Mi Aplicación</h1>
        
        <form id="miFormulario">
            <div class="form-group">
                <label for="nombre">Nombre:</label>
                <input type="text" id="nombre" name="nombre" placeholder="Ingresa tu nombre" required>
            </div>

            <div class="form-group">
                <label for="edad">Edad:</label>
                <input type="number" id="edad" name="edad" placeholder="Ingresa tu edad" required>
            </div>

            <div class="form-group">
                <label for="mensaje">Mensaje:</label>
                <textarea id="mensaje" name="mensaje" rows="4" placeholder="Escribe un mensaje..."></textarea>
            </div>

            <button type="submit">Guardar</button>
        </form>

        <div class="resultado" id="resultado">
            <h2>Información Guardada:</h2>
            <p><strong>Nombre:</strong> <span id="nombreMuestra"></span></p>
            <p><strong>Edad:</strong> <span id="edadMuestra"></span></p>
            <p><strong>Mensaje:</strong> <span id="mensajeMuestra"></span></p>
        </div>
    </div>

    <script>
        // Recuperar datos guardados cuando se carga la página
        window.addEventListener('load', function() {
            const datosGuardados = localStorage.getItem('misDatos');
            if (datosGuardados) {
                const datos = JSON.parse(datosGuardados);
                document.getElementById('nombreMuestra').textContent = datos.nombre;
                document.getElementById('edadMuestra').textContent = datos.edad;
                document.getElementById('mensajeMuestra').textContent = datos.mensaje;
                document.getElementById('resultado').classList.add('activo');
            }
        });

        // Procesar el formulario
        document.getElementById('miFormulario').addEventListener('submit', function(e) {
            e.preventDefault();

            const datos = {
                nombre: document.getElementById('nombre').value,
                edad: document.getElementById('edad').value,
                mensaje: document.getElementById('mensaje').value
            };

            // Guardar en memoria local (sin internet)
            localStorage.setItem('misDatos', JSON.stringify(datos));

            // Mostrar resultado
            document.getElementById('nombreMuestra').textContent = datos.nombre;
            document.getElementById('edadMuestra').textContent = datos.edad;
            document.getElementById('mensajeMuestra').textContent = datos.mensaje;
            document.getElementById('resultado').classList.add('activo');

            alert('✅ Datos guardados correctamente');
        });
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Axiombyte</title>

    <!-- Firebase SDK -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js";
        import { getAuth, signInWithEmailAndPassword, GoogleAuthProvider, signInWithPopup } from "https://www.gstatic.com/firebasejs/9.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, getDocs } from "https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore.js";
        import { getAnalytics } from "https://www.gstatic.com/firebasejs/9.6.1/firebase-analytics.js";

        // Configuración de Firebase
        const firebaseConfig = {
            apiKey: "AIzaSyC-95EuJe0aeTCargsELHNHzkX1vsA6fM0",
            authDomain: "axiombyte-57f45.firebaseapp.com",
            projectId: "axiombyte-57f45",
            storageBucket: "axiombyte-57f45.appspot.com",
            messagingSenderId: "267627942381",
            appId: "1:267627942381:web:4e02074e2cecf2ba3397e4",
            measurementId: "G-LHNT01CXQN"
        };

        // Inicializar Firebase
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);
        const analytics = getAnalytics(app);

        // Función para iniciar sesión
        function login() {
            const email = document.getElementById("email").value;
            const password = document.getElementById("password").value;

            if (!email || !password) {
                alert("Por favor complete todos los campos.");
                return;
            }

            signInWithEmailAndPassword(auth, email, password)
                .then((userCredential) => {
                    alert('¡Inicio de sesión exitoso!');
                    window.location.hash = "catalogo"; // Cambia la vista a la página del catálogo
                })
                .catch((error) => {
                    alert("Error en el inicio de sesión: " + error.message);
                });
        }

        // Función para iniciar sesión con Google
        function loginWithGoogle() {
            const provider = new GoogleAuthProvider();
            signInWithPopup(auth, provider)
                .then((result) => {
                    alert('¡Inicio de sesión con Google exitoso!');
                    window.location.hash = "catalogo"; // Cambia la vista a la página del catálogo
                })
                .catch((error) => {
                    alert("Error en el inicio de sesión con Google: " + error.message);
                });
        }

        // Exponer funciones al ámbito global
        window.login = login;
        window.loginWithGoogle = loginWithGoogle;
    </script>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #9B4DFF, #00FFFF);
            color: white;
            margin: 0;
            padding: 0;
        }
        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            max-width: 1000px;
            margin: auto;
            padding: 20px;
        }
        h1 {
            margin-bottom: 20px;
            cursor: pointer; /* Hacer que el título sea clickeable */
        }
        .form-container {
            background: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            width: 100%;
            max-width: 500px;
            text-align: center;
        }
        input, button {
            padding: 10px;
            margin: 10px 0;
            width: 100%;
            border-radius: 5px;
            border: none;
        }
        button {
            background: #00FFFF;
            color: black;
            cursor: pointer;
        }
        /* Estilos para las "ventanas" */
        .catalogo-container, .inicio-container, .invitado-container {
            display: none;
        }
        .active {
            display: block;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Hacemos que el título sea un enlace -->
        <h1 onclick="redirectToGuest()">Axiombyte</h1>

        <!-- Página de Invitado -->
        <div id="invitado" class="invitado-container">
            <h2>Bienvenido, Invitado</h2>
            <p>Explora el contenido como invitado.</p>
            <button onclick="window.location.hash = 'inicio'">Ir a Inicio de Sesión</button>
        </div>

        <!-- Página de Inicio -->
        <div id="inicio" class="form-container active">
            <h2>Registro / Ingreso</h2>
            <input type="text" id="email" placeholder="Correo" required>
            <input type="password" id="password" placeholder="Contraseña" required>
            <button onclick="login()">Iniciar Sesión</button>
            <button onclick="loginWithGoogle()">Iniciar con Google</button>
        </div>

        <!-- Página del Catálogo -->
        <div id="catalogo" class="catalogo-container">
            <h2>Bienvenido al Catálogo</h2>
            <p>¡Explora nuestros productos!</p>
        </div>
    </div>

    <script>
        // Función para redirigir al área de "invitado" al hacer clic en Axiombyte
        function redirectToGuest() {
            window.location.hash = 'invitado';
        }

        // Detecta cambios en la URL para manejar las "ventanas"
        window.addEventListener('hashchange', () => {
            const hash = window.location.hash.substring(1); // Obtiene la parte después de #
            
            // Ocultar todas las secciones
            document.querySelectorAll('.form-container, .catalogo-container, .invitado-container').forEach(section => {
                section.classList.remove('active');
            });
            
            // Mostrar la sección correspondiente
            if (hash === 'catalogo') {
                document.getElementById('catalogo').classList.add('active');
            } else if (hash === 'invitado') {
                document.getElementById('invitado').classList.add('active');
            } else {
                document.getElementById('inicio').classList.add('active');
            }
        });
        
        // Llama al cambio inicial de hash
        if (window.location.hash) {
            window.dispatchEvent(new HashChangeEvent('hashchange'));
        }
    </script>
</body>
</html># webb
Axiombyte

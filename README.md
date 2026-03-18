# 🍃 LARAVEL DESDE CERO - GUÍA COMPLETA

**Laravel desde Cero** es un sitio educativo completo diseñado para enseñar Laravel desde los fundamentos hasta conceptos avanzados, con explicaciones claras, ejemplos prácticos y código listo para usar.

> *"Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience."*

---

## 🎯 ¿Qué es este Proyecto?

Este proyecto proporciona un recurso educativo gratuito para aprender Laravel, incluyendo:

- **Documentación completa** de cada tema
- **Ejemplos de código** listos para ejecutar
- **Ejercicios prácticos** para reforzar el aprendizaje
- **Sitio web educativo** con navegación intuitiva

---

## 📚 Contenido del Curso

### Módulo 1: Fundamentos

1. **Introducción**
   - ¿Qué es Laravel?
   - MVC Pattern
   - Ecosistema Laravel

2. **Instalación**
   - Composer y requisitos
   - Laravel Installer
   - Estructura de proyecto
   - Configuración de entorno

3. **Conceptos básicos**
   - Routing
   - Controllers
   - Views con Blade
   - Models y Eloquent

### Módulo 2: Intermedio

4. **Ejemplos prácticos**
   - Migraciones y seeders
   - Formularios y validación
   - Autenticación
   - Middleware

5. **Buenas prácticas**
   - Service Container
   - Service Providers
   - Eventos y Listeners
   - Testing con PHPUnit

### Módulo 3: Avanzado

6. **Casos reales**
   - APIs RESTful
   - Laravel Sanctum/Passport
   - Colas y Jobs
   - Notificaciones

7. **Proyecto final**
   - Aplicación completa
   - Deploy a producción
   - CI/CD pipeline

---

## 🗂️ Estructura del Proyecto

```
Practica-Orden-n-merico/
├── index.html          # Página principal
├── css/
│   └── styles.css      # Estilos del sitio
├── js/
│   └── main.js         # JavaScript del sitio
└── README.md
```

---

## 🚀 Cómo Usar este Proyecto

### Opción 1: Navegar el Sitio Web

1. Abre `index.html` en tu navegador
2. Navega por las secciones del curso
3. Haz clic en los temas para ver la documentación detallada

### Opción 2: Ejecutar los Ejemplos

1. Instala Composer y PHP
2. Crea proyecto Laravel
3. Ejecuta con `php artisan serve`

### Requisitos

- PHP 8.1+
- Composer
- Node.js y npm

---

## 📝 Ejemplos Rápidos

### Rutas

```php
// routes/web.php

use App\Http\Controllers\UserController;

// Ruta básica
Route::get('/', function () {
    return view('welcome');
});

// Ruta con parámetro
Route::get('/user/{id}', function ($id) {
    return "User $id";
});

// Ruta con controller
Route::get('/users', [UserController::class, 'index']);

// Route group con middleware
Route::middleware(['auth'])->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index']);
});
```

### Controller

```php
<?php

namespace App\Http\Controllers;

use App\Models\User;
use Illuminate\Http\Request;

class UserController extends Controller
{
    public function index()
    {
        $users = User::paginate(10);
        return view('users.index', compact('users'));
    }

    public function store(Request $request)
    {
        $validated = $request->validate([
            'name' => 'required|string|max:255',
            'email' => 'required|email|unique:users',
            'password' => 'required|min:8',
        ]);

        $user = User::create($validated);
        return response()->json($user, 201);
    }
}
```

### Eloquent ORM

```php
<?php

use App\Models\User;

// Crear
$user = User::create([
    'name' => 'Juan',
    'email' => 'juan@email.com',
    'password' => bcrypt('password'),
]);

// Leer
$users = User::all();
$user = User::find(1);
$users = User::where('active', true)->get();

// Actualizar
$user->update(['name' => 'Pedro']);

// Eliminar
$user->delete();

// Relaciones
$user->posts()->create(['title' => 'Mi Post']);
$posts = $user->posts;
```

### Migraciones

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('users');
    }
};
```

### Blade Templates

```blade
{{-- resources/views/users/index.blade.php --}}

@extends('layouts.app')

@section('content')
<div class="container">
    <h1>Usuarios</h1>

    @if(session('success'))
        <div class="alert alert-success">
            {{ session('success') }}
        </div>
    @endif

    <table>
        @foreach($users as $user)
            <tr>
                <td>{{ $user->name }}</td>
                <td>{{ $user->email }}</td>
                <td>
                    <a href="{{ route('users.show', $user) }}">Ver</a>
                </td>
            </tr>
        @endforeach
    </table>

    {{ $users->links() }}
</div>
@endsection
```

---

## 🎓 Metodología de Aprendizaje

### 1. Leer la Teoría
Cada tema comienza con una explicación clara del concepto.

### 2. Ver Ejemplos
Los ejemplos de código muestran la aplicación práctica.

### 3. Practicar
Los ejercicios te permiten aplicar lo aprendido.

### 4. Experimentar
Modifica los ejemplos para entender cómo funcionan.

---

## 🔧 Comandos Esenciales

### Artisan CLI

```bash
# Crear proyecto
composer create-project laravel/laravel mi-app

# Servidor de desarrollo
php artisan serve

# Crear controller
php artisan make:controller UserController

# Crear modelo
php artisan make:model User -m

# Ejecutar migraciones
php artisan migrate

# Seed database
php artisan db:seed

# Limpiar caché
php artisan cache:clear
php artisan config:clear
php artisan view:clear

# Listar rutas
php artisan route:list
```

---

## 📖 Recursos Adicionales

### Documentación Oficial

- [Laravel Documentation](https://laravel.com/docs)
- [Laracasts](https://laracasts.com/)
- [Laravel News](https://laravel-news.com/)

### Herramientas Recomendadas

- **Laravel Installer** - CLI oficial
- **Laravel Debugbar** - Debugging
- **Laravel IDE Helper** - Autocompletado

### Comunidades

- [Laravel Community](https://laravel.com/docs/community)
- [Laracasts Forum](https://laracasts.com/discuss)
- [Reddit r/laravel](https://www.reddit.com/r/laravel/)

---

## 💡 Consejos para Principiantes

1. **Sigue la documentación**: Es excelente y actualizada.
2. **Usa Eloquent**: Es poderoso y elegante.
3. **Aprende Service Container**: Es fundamental en Laravel.
4. **Escribe tests**: PHPUnit está integrado.
5. **Explora el ecosistema**: Hay paquetes para todo.

---

## ⚠️ Mejores Prácticas

### Seguridad

- Usa validación en todos los inputs
- Implementa CSRF protection
- Usa prepared statements (Eloquent lo hace)

### Código Limpio

- Sigue PSR-12
- Usa Form Requests para validación compleja
- Mantén controllers delgados

### Rendimiento

- Usa eager loading para relaciones
- Implementa caching
- Usa queue para tareas pesadas

---

## 🧪 Ejercicios Prácticos

### Nivel Básico

1. CRUD de usuarios
2. Sistema de login
3. Blog simple

### Nivel Intermedio

1. API RESTful
2. Sistema de roles y permisos
3. Carrito de compras

### Nivel Avanzado

1. E-commerce completo
2. Sistema multi-tenant
3. Microservicios con Laravel

---

## 👨‍💻 Desarrollado por Isaac Esteban Haro Torres

**Ingeniero en Sistemas · Full Stack · Automatización · Data**

- 📧 Email: zackharo1@gmail.com
- 📱 WhatsApp: 098805517
- 💻 GitHub: https://github.com/ieharo1
- 🌐 Portafolio: https://ieharo1.github.io/portafolio-isaac.haro/

---

© 2026 Isaac Esteban Haro Torres - Todos los derechos reservados.

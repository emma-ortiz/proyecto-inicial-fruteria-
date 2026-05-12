# 📱 Plan de Implementación: "Frutería: Olivos Verdes" (Flutter + Firebase)

> 📌 **Objetivo:** Desarrollar una aplicación multiplataforma (Android, iOS, Web) para gestión de catálogo, autenticación de usuarios y base de datos en tiempo real, utilizando Flutter, Dart, Firebase (Auth + Firestore), Provider y VS Code.

---

## 🛠️ 1. Herramientas y Requisitos Previos

| Categoría | Herramienta | Propósito |
|----------|-------------|-----------|
| **Entorno de Desarrollo** | VS Code + Extensiones (`Flutter`, `Dart`, `Firebase`, `Pubspec Assist`, `GitLens`) | Editor principal, linting, hot reload, gestión de paquetes |
| **SDK & CLI** | Flutter SDK ≥3.16, Dart SDK, Firebase CLI, `flutter doctor` | Compilación, emulación, despliegue, diagnóstico |
| **Emuladores/Simuladores** | Android Studio (AVD), iOS Simulator, Chrome/Edge (Web) | Pruebas multiplataforma |
| **Diseño UI/UX** | Figma / Penpot / Adobe XD | Wireframes, prototipos interactivos, Design System, exportación de assets |
| **Control de Versiones** | Git + GitHub/GitLab | Historial, ramas, CI/CD futuro, colaboración |
| **Gestión de Configuración** | `flutter_dotenv` o variables de entorno nativas | Separar credenciales, URLs, modos (dev/prod) |

> 💡 **Nota:** "Antigravity" no es un IDE reconocido para Flutter. Se recomienda **VS Code** como editor principal y **Android Studio** únicamente para gestionar emuladores y SDKs móviles.

---

## 📐 2. Arquitectura y Estructura del Proyecto

Se utilizará una arquitectura limpia y escalable, alineada con buenas prácticas de Flutter:

```
lib/
├── core/               # Constantes, utilidades, temas, routing, errores
├── data/               # Repositorios, servicios Firebase, DTOs
├── domain/             # Modelos de negocio, casos de uso, interfaces
├── presentation/       # Pantallas, widgets, controladores (Providers)
└── main.dart           # Punto de entrada, inicialización de Firebase/Providers
```

### 🔄 Gestión de Estado
- **Provider** como patrón principal
- `ChangeNotifier` para estado reactivo
- `MultiProvider` en `main.dart` para inyección global
- Separación clara entre lógica de negocio y UI

---

## 📦 3. Dependencias Recomendadas (`pubspec.yaml`)

| Paquete | Versión | Finalidad |
|--------|---------|-----------|
| `firebase_core` | `^2.32.0` | Inicialización de Firebase |
| `firebase_auth` | `^4.20.0` | Autenticación email/password |
| `cloud_firestore` | `^4.17.0` | Base de datos NoSQL en tiempo real |
| `provider` | `^6.1.2` | Inyección de dependencias y estado |
| `intl` | `^0.19.0` | Formateo de fechas, monedas, localización |
| `shared_preferences` | `^2.3.0` | Persistencia ligera (token, preferencias UI) |
| `cached_network_image` | `^3.3.1` | Carga y cacheo de imágenes de productos |
| `uuid` | `^4.5.0` | Generación de IDs únicos para pedidos/carritos |
| `flutter_staggered_grid_view` | `^0.7.0` | Layout optimizado para catálogo |
| `formz` o `validators` | `^0.7.0` / `^3.0.0` | Validación de formularios (opcional) |

> ✅ Se mantendrán las versiones actualizadas mediante `flutter pub outdated` y `pubspec.lock` para consistencia.

---

## 🗺️ 4. Plan de Implementación Paso a Paso

### 🔹 Fase 1: Configuración del Entorno y Proyecto Base
1. Instalar Flutter, Dart y VS Code con extensiones oficiales.
2. Ejecutar `flutter doctor` y resolver dependencias pendientes.
3. Crear proyecto: `flutter create fruteria_olivos_verdes --org com.olivosverdes`
4. Configurar Firebase:
   - Crear proyecto en Firebase Console
   - Habilitar **Authentication** (Email/Password)
   - Habilitar **Firestore Database** (modo prueba inicial)
   - Descargar `google-services.json` (Android) y `GoogleService-Info.plist` (iOS)
   - Ejecutar `flutterfire configure` para generación automática de `firebase_options.dart`
5. Verificar conexión básica y commit inicial en Git.

### 🔹 Fase 2: Diseño UI/UX y Prototipado
1. Definir identidad visual: paleta (verdes, tierra, blanco), tipografía, iconografía, espaciado.
2. Crear wireframes en Figma para:
   - Login / Registro
   - Catálogo de frutas (grid, filtros, búsqueda)
   - Detalle de producto
   - Carrito / Checkout
   - Perfil de usuario
3. Validar flujo de navegación, estados de carga, vacíos y errores.
4. Exportar assets (logos, imágenes placeholder, iconos) y documentar Design System.
5. Definir estrategia responsive (móvil primero, adaptación a tablet/web).

### 🔹 Fase 3: Integración de Firebase (Auth + Firestore)
1. Configurar reglas de seguridad en Firestore:
   - Lectura/escritura limitada a usuarios autenticados
   - Estructura de colecciones: `users`, `products`, `orders`, `carts`
2. Implementar servicio de autenticación:
   - Registro con email/password
   - Inicio de sesión
   - Cierre de sesión y manejo de errores (contraseña débil, email duplicado, etc.)
3. Probar flujos con consola y Firebase Emulator Suite (opcional pero recomendado).
4. Validar persistencia de sesión entre reinicios.

### 🔹 Fase 4: Arquitectura de Estado y Capa de Datos
1. Configurar `pubspec.yaml` con dependencias listadas.
2. Crear modelos de dominio: `User`, `Product`, `CartItem`, `Order`.
3. Implementar servicios de acceso a Firestore (`AuthService`, `FirestoreService`).
4. Crear Providers:
   - `AuthProvider`: estado de sesión, validación, recuperación de contraseña
   - `ProductProvider`: listado, búsqueda, filtros, detalle
   - `CartProvider`: agregar, eliminar, actualizar cantidad, calcular total
5. Vincular providers en `main.dart` con `MultiProvider`.

### 🔹 Fase 5: Desarrollo de Interfaces y Navegación
1. Implementar estructura de routing (rutas nombradas, guards de autenticación).
2. Diseñar pantallas con Material 3 / Cupertino según plataforma.
3. Crear formularios de login/registro con validación en tiempo real.
4. Implementar catálogo con lazy loading, búsqueda y filtros por categoría/precio.
5. Agregar indicadores de carga (`CircularProgressIndicator`), SnackBars para feedback, y manejo de errores de red.
6. Configurar tema global (`ThemeData`) y assets.

### 🔹 Fase 6: Lógica de Negocio y Conectividad en Tiempo Real
1. Conectar UI con Providers usando `context.read()` y `context.watch()`.
2. Implementar streams de Firestore para actualización automática de catálogo y carrito.
3. Validar reglas de negocio:
   - Stock disponible
   - Límite de unidades por producto
   - Precios con descuento/impuestos (si aplica)
4. Implementar flujo de pedido básico (simulado o enlazado a colección `orders`).
5. Manejar desconexiones, reintentos y estado offline (caché local opcional).

### 🔹 Fase 7: Pruebas y Optimización Multiplataforma
1. Pruebas unitarias: lógica de providers, validaciones, cálculos de carrito.
2. Pruebas de widget: renderizado de pantallas, estados de carga/error.
3. Pruebas manuales en:
   - Android (físico + emulador)
   - iOS (simulador)
   - Web (Chrome, responsive, navegación)
4. Optimizar performance:
   - `const` widgets donde sea posible
   - Lazy loading de imágenes y listas
   - Reducción de rebuilds con `Selector`/`Consumer` selectivos
5. Configurar íconos, splash screen, nombres de app y permisos.

### 🔹 Fase 8: Despliegue y Mantenimiento
1. Generar builds:
   - `flutter build apk --release`
   - `flutter build ios --release`
   - `flutter build web --release`
2. Publicar:
   - Google Play Console (APK/AAB)
   - Apple App Store (Xcode archive)
   - Firebase Hosting / Vercel / Netlify (Web)
3. Integrar monitoreo: Firebase Crashlytics, Analytics, Performance Monitoring.
4. Documentar: README técnico, guía de instalación, estructura de Firestore, roadmap v2.

---

## 🔒 5. Consideraciones Críticas y Buenas Prácticas

| Área | Recomendación |
|------|---------------|
| **Seguridad** | Nunca hardcodear credenciales. Usar reglas estrictas en Firestore. Validar entrada en cliente y servidor (Firebase Security Rules). |
| **Estado** | Evitar `setState` para datos compartidos. Usar `Provider` con `ChangeNotifier` y `notifyListeners()` solo cuando sea necesario. |
| **Rendimiento** | Usar `ListView.builder` o `GridView.builder`. Evitar reconstruir widgets innecesariamente. Cache de imágenes. |
| **UX** | Feedback inmediato en acciones. Estados vacíos amigables. Navegación predecible. Accesibilidad (contraste, tamaños de fuente). |
| **Git** | Commits semánticos (`feat:`, `fix:`, `chore:`). Ramas por funcionalidad. Pull Requests con revisión. |
| **Escalabilidad** | Separar lógica de UI. Preparar repos para futuras APIs o pagos. Documentar estructura de Firestore. |

---

## ✅ 6. Siguientes Pasos (Antes del Código)

1. **Validación del plan:** ¿Ajustar fases, agregar funcionalidades (ej. pagos, notificaciones push, panel admin)?
2. **Aprobación de UI/UX:** ¿Ya existen wireframes o requieres una plantilla base en Figma?
3. **Configuración de Firebase:** ¿Tienes cuenta y proyecto listo, o necesitas guía paso a paso para la consola?
4. **Estructura de datos:** ¿Definimos juntos los campos exactos para `users`, `products`, `orders` en Firestore?

> 📝 **Cuando confirmes**, procederé a entregarte:
> - Estructura de carpetas lista para clonar
> - `pubspec.yaml` completo con dependencias y configuración
> - Archivos de inicialización (`main.dart`, `firebase_options.dart`, providers base)
> - Flujo de autenticación sin código de negocio aún (solo esqueleto funcional)

¿Deseas ajustar alguna fase, agregar funcionalidades adicionales o aprobar este plan para comenzar con la Fase 1 + código base?

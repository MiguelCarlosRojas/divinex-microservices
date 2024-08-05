# Estructuración de Repositorios para los Microservicios del Proyecto de Responsabilidad Social de Divinex

Este documento describe la estructura del repositorio, la estrategia de ramificación y las mejores prácticas para aplicar Trunk-Based Development en el versionamiento del código fuente de los microservicios del Proyecto de Responsabilidad Social de Divinex.

## Denominación de Repositorios

Cada microservicio y el frontend tendrán su propio repositorio independiente. La denominación de los repositorios será la siguiente:

- **Backend Microservices:**
  - `vg-ms-accounting`
  - `vg-ms-baptism`
  - `vg-ms-communion`
  - `vg-ms-confirmation`
  - `vg-ms-egress`
  - `vg-ms-income`
  - `vg-ms-marriage`
  - `vg-ms-notification-email`
  - `vg-ms-notification-whatsapp`
  - `vg-ms-storage`
  - `vg-ms-user`

- **Frontend:**
  - `vg-web-divinex`

## Estrategia de Ramificación

### 🌲 Rama Principal (Trunk)
- `main`

La rama principal `main` será el tronco del desarrollo, conteniendo siempre el código más estable y listo para producción.

### 🚀 Ramas de Funcionalidades
- **Convención de Nombres:** `feature/<nombre-de-la-funcionalidad>`

Para el desarrollo de nuevas funcionalidades, se crearán ramas de corta duración desde la rama `main`. Estas ramas serán manejadas de la siguiente manera:
- Cada rama será nombrada siguiendo la convención `feature/<nombre-de-la-funcionalidad>`.
- Las ramas de funcionalidad deberán ser de corta duración, con una duración máxima de unos pocos días.
- Antes de ser fusionadas de vuelta a `main`, se deberá realizar una revisión de código y una integración continua (CI) completa.

### 📦 Ramas de Liberación (Opcional)
- **Convención de Nombres:** `release/<versión>`

Se crearán ramas de liberación desde `main` solo cuando sea necesario estabilizar una versión antes de su liberación. Las ramas de liberación deben ser de corta duración y eliminarse después de la liberación oficial.

### 🛠️ Ramas de Hotfix
- **Convención de Nombres:** `hotfix/<id-del-issue>`

Para correcciones urgentes que afectan directamente a la rama `main`, se crearán ramas de hotfix. Estas ramas seguirán el siguiente proceso:
- Crear una rama de hotfix: `git checkout -b hotfix/<id-del-issue>`
- Aplicar la corrección y probar localmente.
- Empujar a remoto y abrir un PR a `main`.
- Después de revisión, fusionar en `main` y en cualquier rama de liberación relevante.
- Eliminar la rama de hotfix después de la fusión.

## Buenas Prácticas

1. **Integración Continua (CI):**
   - Cada commit en la rama `main` debe pasar por una suite completa de pruebas automáticas (unitarias, de integración, etc.).
   - Configurar un servidor de CI (como Jenkins, CircleCI, TravisCI) para ejecutar estas pruebas automáticamente con cada commit.

2. **Revisión de Código:**
   - Utilizar revisiones de código (Pull Requests) para todas las ramas de funcionalidad antes de fusionarlas a `main`.
   - Asegurar que al menos un desarrollador revise y apruebe los cambios antes de la fusión.

3. **Feature Flags:**
   - Utilizar feature flags para funcionalidades en desarrollo que aún no estén listas para ser liberadas.
   - Esto permite que el código se integre en `main` sin afectar la versión estable de la aplicación.

4. **Commits Frecuentes:**
   - Hacer commits frecuentes y pequeños directamente a la rama `main` o a las ramas de funcionalidad.
   - Asegurar que cada commit sea atómico y pase todas las pruebas locales antes de ser empujado al repositorio.

5. **Automatización de Builds:**
   - Configurar scripts automatizados para construir, probar y desplegar el código.
   - Garantizar que cada commit que llega a `main` sea automáticamente desplegable.

6. **Ramas de Liberación:**
   - Crear ramas de liberación desde `main` solo cuando sea necesario estabilizar una versión antes de su liberación.
   - Las ramas de liberación deben ser de corta duración y eliminarse después de la liberación oficial.

7. **Documentación Clara:**
   - Mantener y actualizar la documentación para cada microservicio con cada cambio significativo.

## Estructura del Repositorio

Cada repositorio tendrá una estructura de directorios similar para mantener la consistencia y facilitar la navegación. Ejemplo de estructura para un microservicio backend (`vg-ms-accounting`):

```
vg-ms-accounting/
├── src/
│   ├── main/
│   │   ├── java/
│   │   ├── resources/
│   ├── test/
│   │   ├── java/
│   │   ├── resources/
├── scripts/
│   ├── build.sh
│   ├── deploy.sh
├── .github/
│   ├── workflows/
│   │   ├── ci.yml
├── README.md
├── pom.xml (o build.gradle)
```

Y para el frontend (`vg-web-divinex`):

```
vg-web-divinex/
├── src/
│   ├── components/
│   ├── pages/
│   ├── styles/
│   ├── assets/
│   ├── index.js
│   ├── App.js
├── public/
├── scripts/
│   ├── build.sh
│   ├── deploy.sh
├── .github/
│   ├── workflows/
│   │   ├── ci.yml
├── README.md
├── package.json
```

## Flujo de Trabajo

### 1. **Iniciar una Nueva Funcionalidad**

```bash
git checkout -b feature/<feature-name>
# Desarrollar la funcionalidad
# Hacer commits de los cambios
```

### 2. **Pruebas Pre-Integración**
Ejecutar todas las pruebas localmente para asegurar que pasen.

### 3. **Revisión de Código**
Empujar la rama de funcionalidad al repositorio remoto.
Abrir un pull request desde `feature/<feature-name>` a `main`.
El equipo revisa y proporciona feedback.
Atender el feedback y hacer los cambios necesarios.

### 4. **Fusionar a Main**
Después de la aprobación del PR y de pasar las pruebas:
```bash
git branch -d feature/<feature-name>
```

### 5. **Proceso de Liberación (Opcional)**

```bash
git checkout -b release/<version>
# Pruebas finales y correcciones
git checkout main
git merge release/<version>
git tag <version>
git branch -d release/<version>
```

Siguiendo esta estructura y prácticas, aseguramos un proceso de desarrollo ágil y eficiente para los microservicios del Proyecto de Responsabilidad Social de Divinex utilizando Trunk-Based Development.

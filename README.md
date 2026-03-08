# 🚀 Neon Flow - Kanban Board

**Neon Flow** es un gestor de tareas de alto rendimiento con estética *Cyberpunk/Dark Mode*. Diseñado para ofrecer una experiencia de usuario fluida, visualmente impactante y totalmente funcional para la gestión de flujos de trabajo personales o de equipo.



---

## 🛠️ Stack Tecnológico

El proyecto está construido bajo los estándares más modernos de desarrollo web:

* **Vue 3 (Composition API):** Reactividad eficiente y código organizado mediante `script setup`.
* **Tailwind CSS:** Diseño responsivo y estilización mediante utilidades de bajo nivel.
* **VueDraggable (Sortable.js):** Motor de arrastre y soltar altamente optimizado.

---

## 🌟 Funcionalidades Clave

### 📋 Gestión de Tareas
* **CRUD Completo:** Crear, leer, actualizar y borrar tareas de forma instantánea.
* **Edición Detallada:** Modal avanzado para gestionar títulos y descripciones.
* **Borrado Rápido:** Botón de eliminación directa en cada tarjeta para optimizar el tiempo.

### 🖱️ Interactividad Avanzada
* **Drag & Drop Fluido:** Movimiento entre columnas con recalculo de posición automático.
* **Layout Anti-Errores:** Estructura de rejilla (Grid) que garantiza zonas de colisión precisas incluso en pantallas Ultra-Wide.
* **Validación en Tiempo Real:** Contadores de caracteres para evitar textos excesivamente largos.

### 🎨 Diseño y UX
* **Glassmorphism:** Efectos de desenfoque de fondo y transparencias.
* **Animaciones:** Transiciones suaves de entrada (`slide-up`) y estados de arrastre (`drag-rotate`).

---

## 📂 Estructura del Código

Para mantener el proyecto limpio y profesional, se ha seguido una arquitectura de **Componentes**:

* **`src/components/`**: Componentes visuales atomizados (Columnas, Tarjetas, Modales).
* **`src/App.vue`**: Orquestador principal que conecta la lógica con la interfaz.

---

## 🚀 Instalación Rápida

1.  **Clonar:**
    ```bash
    git clone [https://github.com/bernal-code/gestorTareas.git]
    ```
2.  **Instalar dependencias:**
    ```bash
    npm install
    ```
3.  **Lanzar servidor de desarrollo:**
    ```bash
    npm run dev
    ```

---
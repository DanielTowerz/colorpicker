# Dynamic Theme Picker 🎨

**[English](#english) | [Español](#español)**

---

## English

A sophisticated dynamic theme picker built with **SvelteKit 5**, **Tailwind CSS 4**, and **OKLCH color space**. This application demonstrates an advanced color system that automatically adapts entire interfaces based on a single color selection, with real-time preview and CSS export functionality.

### ✨ Features

- **🎨 Dynamic Color System**: Choose any base color and watch the entire interface adapt automatically
- **🔧 Advanced Controls**: Fine-tune surface lightness, brand colors, and text opacity with intuitive sliders
- **📱 Responsive Design**: Fixed sidebar on desktop, mobile-friendly overlay with toggle
- **🎯 OKLCH Color Space**: Uses perceptually uniform color calculations for natural color relationships
- **♿ Automatic Accessibility**: Text color automatically switches between black/white for optimal contrast
- **💾 CSS Export**: Generate complete, self-contained CSS files for any project
- **⚡ Real-time Preview**: See changes instantly across all components
- **🔄 Relative Colors**: All colors calculated as mathematical relationships to the base color

### 🚀 Technology Stack

- **SvelteKit 5** with runes (`$state`, `$props`, `$effect`)
- **Tailwind CSS 4** with CSS-first configuration
- **TypeScript** for type safety
- **OKLCH Color Space** for perceptually uniform color manipulation
- **CSS Custom Properties** for dynamic theming
- **PNPM** for fast, efficient package management

### 🏗️ Architecture Highlights

#### Color System
```css
/* Base color chosen by user */
--base-color: #3b82f6;

/* Calculated relative colors */
--surface-color: oklch(from var(--base-color) calc(l * 1.2) c h);
--brand-color: oklch(from var(--base-color) calc(l * 3) calc(c * 5) h);
--text-color: #ffffff; /* Auto-calculated for contrast */
--text-secondary: oklch(from var(--text-color) l c h / 0.6);
```

#### Component Structure
- **ThemePicker**: Core component managing theme state and CSS generation
- **Fixed Sidebar**: Always-accessible theme controls with responsive behavior
- **Demo Components**: Cards, buttons, blog posts showcasing the theme system

### 🛠️ Getting Started

#### Prerequisites
- Node.js 18+ 
- PNPM (recommended) or npm

#### Installation
```bash
# Clone the repository
git clone <repository-url>
cd themepicker

# Install dependencies
pnpm install

# Start development server
pnpm dev

# Open in browser
open http://localhost:5173
```

#### Development Commands
```bash
# Development server
pnpm dev

# Build for production
pnpm build

# Preview production build
pnpm preview

# Type checking
pnpm check

# Type checking in watch mode
pnpm check:watch
```

### 📖 Usage

1. **Select Base Color**: Use the color picker to choose your primary theme color
2. **Adjust Parameters**: Fine-tune surface lightness, brand intensity, and text opacity
3. **Real-time Preview**: Watch the entire interface adapt as you make changes
4. **Export Theme**: Download a complete CSS file with your custom theme
5. **Integrate**: Use the exported CSS in any project with the generated class names

### 🎯 Key Features Explained

#### OKLCH Color Space
Unlike traditional RGB or HSL, OKLCH provides perceptually uniform color manipulation, meaning mathematical changes result in visually consistent adjustments across all hues.

#### Relative Color Calculations
- **Surface Color**: Automatically lighter than base for container backgrounds
- **Brand Color**: High-contrast version for buttons and emphasis
- **Text Colors**: Automatically calculated for optimal readability
- **All Relationships**: Maintained across any base color choice

#### Responsive Design
- **Desktop/Tablet**: Fixed sidebar (380px/320px) with content margin
- **Mobile**: Hidden sidebar with toggle button, slides in from right
- **Accessibility**: All controls remain keyboard accessible

### 🔧 Customization

The theme system supports extensive customization:

- **Surface Lightness**: 0.5x to 2.0x base color lightness
- **Brand Lightness**: 1.0x to 5.0x base color lightness  
- **Brand Chroma**: 1.0x to 10.0x base color saturation
- **Text Opacity**: 10% to 100% for secondary text

### 📚 Technical Details

#### Browser Support
- **Chrome 111+**, **Firefox 128+**, **Safari 16.4+**
- Requires modern CSS features: `@property`, `color-mix()`, relative color functions

#### Performance
- CSS custom properties update in real-time
- No JavaScript color calculations during runtime
- Efficient DOM updates with Svelte 5 fine-grained reactivity

### 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## Español

Un selector de temas dinámico sofisticado construido con **SvelteKit 5**, **Tailwind CSS 4** y **espacio de color OKLCH**. Esta aplicación demuestra un sistema de colores avanzado que adapta automáticamente interfaces completas basándose en la selección de un solo color, con vista previa en tiempo real y funcionalidad de exportación CSS.

### ✨ Características

- **🎨 Sistema de Colores Dinámico**: Elige cualquier color base y observa cómo toda la interfaz se adapta automáticamente
- **🔧 Controles Avanzados**: Ajusta finamente la luminosidad de superficie, colores de marca y opacidad de texto con deslizadores intuitivos
- **📱 Diseño Responsivo**: Barra lateral fija en escritorio, overlay amigable para móviles con botón de alternancia
- **🎯 Espacio de Color OKLCH**: Utiliza cálculos de color perceptualmente uniformes para relaciones de color naturales
- **♿ Accesibilidad Automática**: El color del texto cambia automáticamente entre negro/blanco para contraste óptimo
- **💾 Exportación CSS**: Genera archivos CSS completos y autónomos para cualquier proyecto
- **⚡ Vista Previa en Tiempo Real**: Ve los cambios instantáneamente en todos los componentes
- **🔄 Colores Relativos**: Todos los colores calculados como relaciones matemáticas al color base

### 🚀 Stack Tecnológico

- **SvelteKit 5** con runes (`$state`, `$props`, `$effect`)
- **Tailwind CSS 4** con configuración CSS-first
- **TypeScript** para seguridad de tipos
- **Espacio de Color OKLCH** para manipulación de color perceptualmente uniforme
- **Propiedades Personalizadas CSS** para tematización dinámica
- **PNPM** para gestión de paquetes rápida y eficiente

### 🏗️ Aspectos Arquitectónicos Destacados

#### Sistema de Colores
```css
/* Color base elegido por el usuario */
--base-color: #3b82f6;

/* Colores relativos calculados */
--surface-color: oklch(from var(--base-color) calc(l * 1.2) c h);
--brand-color: oklch(from var(--base-color) calc(l * 3) calc(c * 5) h);
--text-color: #ffffff; /* Auto-calculado para contraste */
--text-secondary: oklch(from var(--text-color) l c h / 0.6);
```

#### Estructura de Componentes
- **ThemePicker**: Componente principal que gestiona el estado del tema y generación CSS
- **Barra Lateral Fija**: Controles de tema siempre accesibles con comportamiento responsivo
- **Componentes Demo**: Tarjetas, botones, posts de blog que muestran el sistema de temas

### 🛠️ Comenzando

#### Requisitos Previos
- Node.js 18+
- PNPM (recomendado) o npm

#### Instalación
```bash
# Clonar el repositorio
git clone <url-del-repositorio>
cd themepicker

# Instalar dependencias
pnpm install

# Iniciar servidor de desarrollo
pnpm dev

# Abrir en navegador
open http://localhost:5173
```

#### Comandos de Desarrollo
```bash
# Servidor de desarrollo
pnpm dev

# Construir para producción
pnpm build

# Vista previa de construcción de producción
pnpm preview

# Verificación de tipos
pnpm check

# Verificación de tipos en modo observación
pnpm check:watch
```

### 📖 Uso

1. **Seleccionar Color Base**: Usa el selector de color para elegir tu color de tema principal
2. **Ajustar Parámetros**: Ajusta finamente la luminosidad de superficie, intensidad de marca y opacidad de texto
3. **Vista Previa en Tiempo Real**: Observa cómo toda la interfaz se adapta mientras haces cambios
4. **Exportar Tema**: Descarga un archivo CSS completo con tu tema personalizado
5. **Integrar**: Usa el CSS exportado en cualquier proyecto con los nombres de clase generados

### 🎯 Características Clave Explicadas

#### Espacio de Color OKLCH
A diferencia del tradicional RGB o HSL, OKLCH proporciona manipulación de color perceptualmente uniforme, lo que significa que los cambios matemáticos resultan en ajustes visualmente consistentes a través de todos los matices.

#### Cálculos de Color Relativos
- **Color de Superficie**: Automáticamente más claro que la base para fondos de contenedores
- **Color de Marca**: Versión de alto contraste para botones y énfasis
- **Colores de Texto**: Calculados automáticamente para legibilidad óptima
- **Todas las Relaciones**: Mantenidas a través de cualquier elección de color base

#### Diseño Responsivo
- **Escritorio/Tablet**: Barra lateral fija (380px/320px) con margen de contenido
- **Móvil**: Barra lateral oculta con botón de alternancia, se desliza desde la derecha
- **Accesibilidad**: Todos los controles permanecen accesibles por teclado

### 🔧 Personalización

El sistema de temas soporta personalización extensa:

- **Luminosidad de Superficie**: 0.5x a 2.0x luminosidad del color base
- **Luminosidad de Marca**: 1.0x a 5.0x luminosidad del color base
- **Croma de Marca**: 1.0x a 10.0x saturación del color base
- **Opacidad de Texto**: 10% a 100% para texto secundario

### 📚 Detalles Técnicos

#### Soporte de Navegadores
- **Chrome 111+**, **Firefox 128+**, **Safari 16.4+**
- Requiere características CSS modernas: `@property`, `color-mix()`, funciones de color relativas

#### Rendimiento
- Las propiedades personalizadas CSS se actualizan en tiempo real
- Sin cálculos de color JavaScript durante el tiempo de ejecución
- Actualizaciones DOM eficientes con reactividad fina de Svelte 5

### 🤝 Contribuyendo

1. Haz fork del repositorio
2. Crea una rama de característica (`git checkout -b feature/caracteristica-increible`)
3. Confirma tus cambios (`git commit -m 'Agregar característica increíble'`)
4. Push a la rama (`git push origin feature/caracteristica-increible`)
5. Abre un Pull Request

### 📄 Licencia

Este proyecto es código abierto y está disponible bajo la [Licencia MIT](LICENSE).

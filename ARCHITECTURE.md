# Arquitectura del Proyecto: EcoTech Solutions - Inventario Sostenible

## 1. Visión General de la Arquitectura
Este proyecto utiliza **React** con **TypeScript** como stack principal para la construcción de una interfaz de usuario escalable, robusta y predecible. La adopción de TypeScript garantiza la detección temprana de errores mediante un tipado estricto, mejorando la mantenibilidad a largo plazo y facilitando el onboarding de nuevos desarrolladores al ofrecer un código autodocumentado.

## 2. Separación de Preocupaciones (Separation of Concerns)
Para asegurar que el código sea mantenible y fácil de probar, hemos diseñado la arquitectura dividiendo estrictamente el proyecto en las siguientes capas funcionales:

- **UI / Presentación (`src/components/`):** Contiene componentes visuales puros (Dumb/Presentational Components). Estos componentes no tienen conocimiento del origen de los datos ni de la lógica de negocio; su única responsabilidad es renderizar la información basándose en las *props* que reciben y notificar eventos a capas superiores.
- **Lógica de Vista (`src/hooks/`):** A través de Custom Hooks se encapsula la gestión de estado y la orquestación de la UI. De este modo, extraemos la complejidad de los componentes, permitiendo que la lógica pueda ser testeada y reutilizada en distintos contextos visuales.
- **Capa de Servicios (`src/services/`):** Esta capa contiene exclusivamente las llamadas a bases de datos y a otras APIs externas. Ningún componente o hook interactúa directamente con la red sin pasar por los servicios correspondientes.
- **Tipado y Entidades (`src/types/`):** Almacenamos aquí las definiciones globales, interfaces y tipos de TypeScript para mantener la consistencia del dominio a lo largo de toda la aplicación.

## 3. Integración Aislada con Supabase
Uno de los puntos clave en nuestra arquitectura es el aislamiento completo de Supabase dentro de `src/services/supabase/`. Esta decisión técnica persigue dos objetivos principales:

1. **Prevención de Deuda Técnica:** Al agrupar el SDK de Supabase, la inicialización del cliente (`client.ts`) y todas las consultas directas en un único módulo, evitamos que los desarrolladores (especialmente perfiles junior) acoplen llamadas a la base de datos dentro de los componentes de React. Si en el futuro es necesario migrar a otra base de datos o modificar la lógica de persistencia, los cambios se limitarán exclusivamente a este directorio, sin afectar la interfaz.
2. **Seguridad y Trazabilidad:** Al mantener centralizada la conexión, aseguramos una correcta inyección de las variables de entorno y un manejo de errores uniforme para todas las transacciones de datos de la plataforma.

Esta estructura Modular bajo los principios de *Separation of Concerns* sentará las bases para construir nuevas funcionalidades de manera ágil y sostenible.

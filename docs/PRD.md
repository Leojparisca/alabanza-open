# PRD — Alabanza Open

Documento de requerimientos de producto. Fuente única de verdad del proyecto.
Si algo no está aquí, no existe como requisito.

## 1. Visión

Alternativa open source a las apps de gestión de equipos de alabanza
(OnStage, Planning Center y similares): sin muros de pago por usuario,
en español y autoalojable. Nace en Valle de la Pascua, Venezuela,
para un equipo de 50 personas con presupuesto cero.

## 2. Usuarios objetivo

- Director de alabanza: planifica servicios, asigna roles y canciones.
- Músico / vocalista: consulta sus servicios, acordes en su tono y audios.
- Iglesias pequeñas sin capacidad de pagar SaaS eclesiástico.

## 3. Principios de producto (innegociables)

1. Sin IA dentro del producto: toda función crítica es determinística
   (la transposición de acordes es un algoritmo, no un modelo).
2. Sin muros de pago ni límites por usuario.
3. Español primero: toda la interfaz nace en español.
4. Mobile-first: el músico la usa en su teléfono en ensayo y en culto.
5. Autoalojable: instalable en servidor propio con documentación clara.
6. Licencia MIT.

## 4. Nomenclatura oficial de estados de un Servicio

- Planificación: se está armando; NO visible para el equipo.
- En Curso: confirmado; visible para el equipo.
- Completado: ya ocurrió; archivado.

## 5. Hoja de ruta por milestones

- M1 (COMPLETADO): scaffold Next.js + Prisma/SQLite + esquema + seed.
- M2: CRUD administrativo interno (Miembros, Canciones, Servicios).
- M3: Planificador de servicios (asignar miembros y canciones con
  posición y tono; disponibilidad simple).
- M4: Vista del músico (enlace por servicio; acordes con transposición
  en vivo usando chord-transposer; audio de referencia).
- M5: Modo On Stage (alto contraste, auto-scroll por BPM, tamaño de
  fuente ajustable) y metrónomo visual.
- M6: Notificaciones (email primero; WhatsApp Cloud API después como
  módulo opcional desmontable).
- M7+: exportación a FreeShow, reglas de rotación, anotaciones
  personales por canción, instalación como PWA.

## 6. Modelo de datos actual (Prisma)

- Miembro: id, nombre, fotoUrl?, email?, whatsapp?, tipoVoz?, rol,
  estado (default "Activo"), createdAt
- Cancion: id, titulo, artista?, tonoOriginal, bpm?, letra?, acordes?,
  audioUrl?, vecesCantada (default 0)
- Servicio: id, fecha, tipo, estado (default "Planificacion"), notas?
- ServicioCancion: id, servicioId, cancionId, posicion, tonoAsignado?
- ServicioMiembro: id, servicioId, miembroId, rolEnServicio,
  confirmado (default false)

Futuros (no construir antes de su milestone): Disponibilidad,
ReglaRotacion, NotaPersonal.

## 7. No-goals explícitos

- IA dentro del producto.
- Apps nativas iOS/Android (se usará PWA).
- Multi-iglesia / multi-tenant en esta fase.
- Pagos, donaciones o monetización interna.
- Edición colaborativa en tiempo real.

## 8. Gobernanza

- Sesiones de 90 minutos; un milestone por sesión.
- Toda sesión cierra con git add + commit + push.
- El agente OpenCode no agrega dependencias que no estén listadas en
  este PRD y anota cada decisión ambigua en docs/DECISIONS.md.
- Los criterios de aceptación los verifica el product owner
  (Leonard) sin leer código.
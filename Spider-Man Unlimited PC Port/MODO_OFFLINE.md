# Modo local sin conexion

La tienda de esta version usa el inventario original y descuenta los viales de la partida. No utiliza compras con dinero real ni responde como si existiera el servidor de Gameloft.

## Como abrirla

- En el menu principal, pulsa **Tienda** o **Reclutar**.
- Tambien puedes pulsar **F3** en el menu principal o en **Mi equipo**.
- Busca un personaje u objeto, seleccionalo y pulsa **Comprar con viales**. Confirma el precio antes de comprar.
- **Volver al juego** cierra la tienda y reanuda el motor original.
- **Mi equipo** permite consultar y usar el inventario sin el bloqueo de conexion.

## Precios iniciales

| Producto | Viales |
| --- | ---: |
| Potenciador de combo | 750 |
| Adrenalina | 750 |
| Mejora de vida | 1.000 |
| Aumento de rango | 5.000 |
| 10 ISO-8 | 5.000 |
| 1 llave | 1.500 |
| Personaje de rareza 1 | 1.000 |
| Personaje de rareza 2 | 3.000 |
| Personaje de rareza 3 | 8.000 |
| Personaje de rareza 4 | 20.000 |
| Personaje de rareza 5 | 45.000 |
| Personaje de rareza 6 | 90.000 |
| Personaje de rareza 7 | 150.000 |

El catalogo se obtiene de tu GameData.json. En la cache compatible hay 426 personajes incluidos y seis productos de objetos/monedas. No se cobra de nuevo por un personaje que ya tienes. No se venden paquetes de viales a cambio de viales ni fichas de alianza que dependan de servicios ausentes. El traje Civil War Peter Parker de rareza 6 queda fuera: su modelo no esta en esta cache.

## Guardado

Se mantiene el formato cifrado original de player.dat. Cada compra valida el saldo, genera y verifica el nuevo guardado, conserva una copia anterior en **Saves/internal/offline/antes-....dat** y sustituye el archivo de forma atomica antes de aplicar la compra en memoria. Si falla la escritura, no se descuenta el saldo. Las pruebas se hicieron sobre copias; la instalacion no recibe monedas, personajes ni partidas de prueba.

## Alcance

Este cambio adapta la tienda y el inventario local. Conserva la progresion de historia. Los eventos del servidor, clasificaciones y alianzas no quedan restaurados con este cambio; necesitan una implementacion y datos propios. Se ocultan los candados laterales del menu y los bloqueos visuales de la barra superior. Esto no sustituye los datos ausentes de los eventos o las alianzas.

Se conservan los controles, pantalla completa, audio y launcher anteriores. La biblioteca del juego y sus recursos se siguen importando desde el APK y OBB/cache del usuario.

## Ascender y portal estandar originales

El boton Ascender de la ficha del personaje procesa el rango localmente y actualiza el poder total del equipo. Usa los requisitos, coste en viales y poder de Ranks en GameData.json; respeta el rango maximo y el objeto de aumento de rango cuando lo eliges.

La compra de 3.000 viales de Standard Rookie se resuelve sin red tanto desde Reclutar como desde la pantalla detallada que abre Conseguir de un portal en la ficha de Ascender. Sortea una de las seis recompensas de su tabla local, entrega el personaje y sus fragmentos, o suma fragmentos si ya lo tienes. Los duplicados de un personaje con rango maximo se convierten en viales segun VialExtraDuplicate. La confirmacion de esa compra aparece en una ventana de Windows. Los demas portales mantienen su comportamiento anterior.

Ambas operaciones comprueban el saldo y guardan antes de aplicar los cambios. Se oculta el indicador visual de falta de conexion; el estado real de red sigue sin alterarse.

### Conseguir de un portal desde Ascender

El boton de 3.000 viales de esa vista detallada usa la misma compra local y
el mismo guardado que Standard Rookie en Reclutar. La confirmacion aparece
en una ventana de Windows. Un personaje nuevo aumenta el poder del inventario;
si recibes fragmentos repetidos, usalos para Ascender al personaje cuando
reunas lo necesario. Se mantienen las probabilidades y el requisito de poder
de la mision (por ejemplo, 21,7); esta correccion no garantiza un personaje
nuevo en cada apertura ni modifica el requisito para entrar a una mision.

## Gold VIP con viales

En la vista de **Gold VIP**, pulsa **Desbloquear**. Se muestra el precio, tu
saldo y la confirmacion de compra: **75.000 viales por una apertura**. No hay
un pago de desbloqueo aparte. Cancelar o no tener saldo suficiente no cobra
nada. El precio equivale al 83,3 % de los 90.000 viales que cuesta elegir
un personaje de rareza 6 en la tienda local; la diferencia compensa el sorteo.

Cada apertura entrega un personaje de rango 1 de los seis que se muestran
en el grupo inicial de Gold VIP: Combat Mode Iron Spider, Guardian, Aaron
Davis, The Other, Venom Klyntar y el traje simbiotico nuevo. Se mantienen
los pesos de su tabla local y se excluyen los que ya tienes. Al completar
esos seis, no se realizan mas cargos en este grupo. No se activa una
suscripcion ni el estado de cliente de pago del antiguo servicio.

La recompensa, sus fragmentos iniciales y el aumento de poder quedan en
el guardado original. Se conserva una copia previa antes de cada compra;
si falla el guardado, no se cobra ni se entrega el personaje. Esta adaptacion
corresponde a Gold VIP: Silver, Platinum y otros portales mantienen su
comportamiento anterior.

## ISO-8 con cantidad ajustable

El boton + de ISO-8 abre una tienda local. Si no tienes los ISO-8 necesarios
para recuperar resistencia, el boton de recuperacion abre esta misma tienda.
El precio es **500 viales por cada ISO-8**, igual que el paquete anterior de
10 por 5.000. Puedes escribir una cantidad o usar los botones - y +; el total
se actualiza antes de confirmar. Por ejemplo, 3 ISO-8 cuestan 1.500 viales.

La primera entrada entrega **5 ISO-8 gratis una sola vez por partida**.
No requiere una compra. El registro del regalo queda en
Saves/internal/pc_iso8_welcome_v1.dat, junto al guardado: conserva toda la
carpeta Saves al mover o respaldar la partida. Volver a abrir la tienda o
reiniciar el juego no vuelve a dar el regalo.

La compra descuenta viales y suma ISO-8 en un solo guardado cifrado original.
Cancelar, introducir una cantidad no valida o no tener suficientes viales no
realiza una compra. Si Windows no permite guardar, no se aplica el cargo.
No se incluyen saldos ni partidas de prueba en la instalacion o el ZIP.

## Resistencia y recompensas sin conexion

El boton original de recuperar resistencia usa los ISO-8 de tu partida.
Mantiene el precio calculado por el motor (por ejemplo, 5 ISO-8 para el
caso comprobado con cuatro personajes). La recuperacion y el gasto se guardan
juntos antes de aplicarse. Si el saldo no alcanza, se abre la tienda local
de ISO-8. Una recuperacion repetida cuando el equipo ya esta lleno no cobra.

Las series de historia entregan sus ISO-8 sin esperar al servidor. Se usan
Issue1CompleteReward a Issue6CompleteReward del GameData del usuario: 6, 10,
15, 20, 25 y 30 ISO-8 en la cache comprobada. Tambien se recupera el premio
pendiente de una serie ya terminada, como los 6 ISO-8 de la primera. Se
comprueba la primera medalla de su jefe final y se registra el cobro por
serie. Repetir niveles o reiniciar no repite ese premio.

En Objetivos, los botones originales Reclamar de oro, plata y bronce
entregan lo que indique el desafio guardado, por ejemplo 3 ISO-8 o 1.000
viales. Se comprueba que el objetivo este completado y se marca como
recogido en el mismo guardado que el premio. Al cambiar la fecha local del
PC se reinician su progreso y su reclamacion; se mantienen sus objetivos.
La primera actualizacion conserva los desafios pendientes de reclamar.

Pulsa **F6** para abrir el regalo por entrar cada dia. El acceso original
al calendario tambien se redirige a este regalo local. Hay confirmacion
antes de reclamar. Usa en ciclo los 31 dias del ultimo calendario original
incluido en la cache (diciembre de 2018), empezando por el dia 1; solo se
avanza al reclamar. No requiere dias consecutivos ni entrega los dias que
no hayas entrado. Los portales de regalo se abren directamente con su tabla
local y entregan un personaje o fragmentos, sin dejar un vale que requiera
al servidor. Conservan las probabilidades entre recursos disponibles.

El registro PCOfflineV1 queda dentro del player.dat cifrado original y se
conserva tambien en los guardados automaticos del motor. El regalo, la fecha
y el saldo se guardan juntos; un fallo de escritura no cobra ni marca la
recompensa como recibida. Conserva la carpeta Saves y esta version del port;
las versiones antiguas no conocen este registro adicional.

Las alianzas, los anuncios y las clasificaciones contra otros jugadores
mantienen su alcance anterior; este cambio adapta las recompensas locales,
no recupera los antiguos servicios de Gameloft.

## Correccion de tienda y ascenso
La tienda local se abre al activar el boton Tienda del juego original (o F3).
Se retiraron los atajos por rectangulos de la pantalla: monedas, Reclutar,
Mi equipo y Retroceder ya no abren la tienda por coincidir con esas zonas.
Durante el ascenso se oculta la cuadricula de cartas como en el callback
original de exito. DisableUserLocation ya tiene su adaptacion para Windows,
sin registrar servicios de ubicacion de Android.

## Consulta de ubicacion al regresar al menu
El host devuelve permiso Android de ubicacion deshabilitado y solicitud no
concedida. Esta ruta del motor ya no se detiene en PermissionPlugin al volver
a los menus. Las consultas y solicitudes se atienden en las tres variantes
JNI; no se modifica la partida ni se habilita un servicio de ubicacion.

## Rendimiento de las comprobaciones offline
Las comprobaciones automaticas de recompensas pendientes y cambio de dia se
realizan al estar visible el menu principal. Se aplazan durante carreras,
combates e introducciones. Los botones de reclamar y el premio de fin de
serie siguen entregando y guardando sus recompensas.
Las seis definiciones de premios se leen una vez por sesion. Si modificas
GameData.json, reinicia el juego para aplicar esos cambios.
El registro PC se incorpora al JSON original del guardado sin volver a
construir todo su arbol; se conserva una ruta compatible de respaldo.

Los streams FILE del adaptador escriben directamente con WriteFile: fflush
ya no fuerza una barrera fisica de disco en cada archivo de seguimiento.
Las transacciones offline conservan su FlushFileBuffers explicito y su
sustitucion del archivo, incluidas las comprobaciones de error de escritura.

## Idiomas de las funciones locales

Las tiendas locales, ISO-8, Gold VIP, precios, compras, ascenso, resistencia y avisos de recompensas usan el idioma elegido para el juego: espanol, ingles, ruso, portugues o frances. Los botones de confirmacion tambien siguen ese idioma. Los precios y el progreso se conservan. Los codigos de diagnostico de los registros mantienen sus nombres.

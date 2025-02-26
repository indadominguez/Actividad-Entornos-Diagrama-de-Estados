# Descripción y Funcionamiento del Diagrama
## Estados:

## 1. EstadoStand_by:

- Descripción: Es el estado inicial y final del sistema. El cajero está inactivo esperando que el usuario realice alguna acción, como insertar la tarjeta.

- Acciones:
  - entry: El sistema se encuentra en espera, sin interactuar con el usuario.
  - do: El sistema permanece inactivo hasta que se realice alguna de las transiciones definidas, como la inserción de la tarjeta.

## 2. VerificarTarjeta:

- Descripción: El sistema verifica la validez de la tarjeta que ha insertado el usuario.
- Acciones:
  - entry: El cajero lee la tarjeta introducida y valida su autenticidad.
  - do: Si la tarjeta es válida, el sistema solicita el PIN; si es inválida, vuelve a esperar una nueva tarjeta o interacción del usuario.

## 3. IntroducirPIN:

- Descripción: El sistema solicita al usuario que ingrese su PIN.
- Acciones:
  - entry: El sistema presenta el campo para que el usuario ingrese su PIN.
  - do: El sistema verifica cada intento de PIN, permitiendo hasta tres intentos antes de bloquear la tarjeta.

## 4. TarjetaBloqueada:

- Descripción: Si el usuario introduce un PIN incorrecto tres veces, el sistema bloquea la tarjeta.
- Acciones:
  - entry: El sistema bloquea la tarjeta y no permite más intentos de acceso.
  - do: No se realizan más transiciones desde este estado, salvo que el usuario reinicie el proceso con una tarjeta nueva.
   
## 5. MenuOperaciones:

- Descripción: El sistema presenta un menú con las opciones de transacciones disponibles después de que el PIN haya sido validado correctamente.
- Acciones:
  - entry: El sistema muestra las opciones de transacción (como retirar dinero, consultar saldo, etc.).
  - do: El sistema espera que el usuario seleccione una operación para llevar a cabo.

## 6. ProcesarOperacion:

- Descripción: El sistema realiza la transacción seleccionada por el usuario.
- Acciones:
  - entry: El sistema inicia el proceso de la operación seleccionada (por ejemplo, retirar dinero).
  - do: El sistema realiza la operación, y al completarla, retorna al menú de operaciones o finaliza la sesión.

---

## Transiciones
## 1. EstadoStand_by --> VerificarTarjeta:

Descripción: La transición ocurre cuando el usuario inserta la tarjeta.
Condición: El cajero detecta la tarjeta y empieza la validación.

## 2. VerificarTarjeta --> EstadoStand_by:

Descripción: Si la tarjeta es inválida, el sistema vuelve al estado de espera (stand-by).
Condición: La tarjeta es rechazada (por ejemplo, si no es válida o está caducada).

## 3. VerificarTarjeta --> IntroducirPIN:

Descripción: Si la tarjeta es válida, el sistema solicita al usuario que ingrese su PIN.

## 4. IntroducirPIN --> IntroducirPIN:

Descripción: El sistema permite que el usuario ingrese el PIN varias veces (hasta tres intentos).
Condición: Si el PIN es incorrecto, el sistema permite reintentar hasta el límite de tres intentos.

## 5. IntroducirPIN --> TarjetaBloqueada:

Descripción: Si el usuario falla tres veces en el intento de introducir el PIN correctamente, la tarjeta se bloquea.
Condición: Después de tres intentos incorrectos.

## 6. IntroducirPIN --> MenuOperaciones:

Descripción: Si el usuario introduce correctamente el PIN, el sistema muestra el menú de opciones de transacciones.
Condición: El PIN es correcto.

## 7. IntroducirPIN --> EstadoStand_by:

Descripción: Si el usuario decide cancelar el proceso de autenticación antes de que se alcance el límite de intentos, el sistema vuelve al estado de espera.
Condición: El usuario cancela la autenticación.

## 8. MenuOperaciones --> ProcesarOperacion:

Descripción: El usuario selecciona una transacción del menú y el sistema procesa la operación.
Condición: El usuario elige una operación (por ejemplo, retirar dinero).

## 9. MenuOperaciones --> EstadoStand_by:

Descripción: El usuario decide cancelar la interacción con el cajero antes de realizar cualquier operación.
Condición: El usuario selecciona la opción de cancelar.

## 10. ProcesarOperacion --> MenuOperaciones:

Descripción: Después de que el sistema haya completado una transacción, se devuelve al menú de operaciones para que el usuario elija otra transacción.
Condición: La transacción se completó con éxito.

## 11. ProcesarOperacion --> EstadoStand_by:

Descripción: Si el usuario decide finalizar la sesión tras completar la operación, el sistema vuelve al estado de espera (stand-by).
Condición: El usuario elige finalizar la sesión.

## 12. TarjetaBloqueada --> [*]:

Descripción: Cuando la tarjeta se bloquea, la sesión se termina y el cajero vuelve al estado inicial, listo para una nueva interacción con otro usuario.

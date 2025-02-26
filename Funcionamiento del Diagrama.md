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

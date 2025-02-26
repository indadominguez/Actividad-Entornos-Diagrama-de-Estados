![image](https://github.com/user-attachments/assets/490f20a7-a24a-407f-a707-41911405f10e)

[*] --> EstadoStand_by

EstadoStand_by --> VerificarTarjeta : Insertar tarjeta
VerificarTarjeta --> EstadoStand_by : Tarjeta inválida
VerificarTarjeta --> IntroducirPIN : Tarjeta válida

IntroducirPIN --> IntroducirPIN : PIN incorrecto (máx. 3 intentos)
IntroducirPIN --> TarjetaBloqueada : 3 intentos fallidos
IntroducirPIN --> MenuOperaciones : PIN correcto
IntroducirPIN --> EstadoStand_by : Cancelar autenticación

TarjetaBloqueada --> [*]

MenuOperaciones --> ProcesarOperacion : Seleccionar operación
MenuOperaciones --> EstadoStand_by : Cancelar interacción

ProcesarOperacion --> MenuOperaciones : Operación completada
ProcesarOperacion --> EstadoStand_by : Finalizar sesión

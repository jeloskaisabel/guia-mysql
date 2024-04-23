# Cursores en MySQL Workbench
#### Elaborado por Grupo 4 INF-272

En `MySQL`, a diferencia de Oracle, para manipular cursores es necesario `crear un procedimiento`, el cual será llamado más adelante para `ejecutar` dicho cursor. A continuación mostramos la `estructura` ideal para cursores explícitos, posteriormente mostraremos un ejemplo en `Workbench`.

## Estructura de Cursores Explícitos
  ```sql
-- Cambiamos el delimitador
DELIMITER $$

-- Definimos el procedimiento
CREATE PROCEDURE EjemploCursorExplicito()
BEGIN
    -- Declaración de variables
    DECLARE done BOOLEAN DEFAULT FALSE;
    DECLARE tempColumn1 INT;
    DECLARE tempColumn2 VARCHAR(255);

    -- Declaración del cursor
    DECLARE cursorTemp CURSOR FOR
        SELECT column1, column2 FROM MiTabla;

    -- Manejador de resultados no encontrados
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    -- Apertura del cursor
    OPEN cursorTemp;

    -- Recorrido de los resultados
    loopTemp: LOOP
        FETCH cursorTemp INTO tempColumn1, tempColumn2;
        
        IF done THEN
            LEAVE loopTemp;
        END IF;
        
        -- Procesamiento de los datos
        -- (Puedes realizar cualquier operación con los datos obtenidos)
    END LOOP;

    -- Cierre del cursor
    CLOSE cursorTemp;
END$$

-- Restauramos el delimitador predeterminado
DELIMITER ;

```
## Ejemplo de Cursor Explicito
![Texto alternativo](ejemplo.png)

1. **Usamos el delimitador:** La instrucción `DELIMITER` se utiliza para cambiar el delimitador de comandos en MySQL.
![Texto alternativo](cursores1.png)

1. **Declaramos las variables:** `done1` es un indicador que nos ayuda a `controlar` si tenemos datos en el cursor.
![Texto alternativo](cursores2.png)
1. **Declaramos el cursor:** para `recorrer` los usuarios.
![Texto alternativo](cursores3.png)

1. **Manejador de resultados no encontrados:** `CONTINUE HANDLER` verifica si ya no existen más registros.
![Texto alternativo](cursores4.png)

1. `Abrimos` el cursor.
![Texto alternativo](cursores5.png)
1. `Recorremos` todos los usuarios devueltos por el `cursor`.
![Texto alternativo](cursores7.png)
1. Obtenemos el `id` del usuario y su `nombre`.
![Texto alternativo](cursores8.png)
1. Inicializamos el `total` de préstamos en `0`.
![Texto alternativo](cursores9.png)
1. `Consultamos` para obtener el total de préstamos del usuario actual e `imprimimos` el `resultado`.
![Texto alternativo](cursores10.png)
1.  `Terminamos` el loop, `cerramos `el cursor y `finalizamos` el procedimiento.
![Texto alternativo](cursores11.png)
1.  `Ejecutamos` el procedimiento con el siguiente comando.
![Texto alternativo](cursores12.png)
1.  Damos `click` para hacer correr el programa al icono de rayo que esta en el `panel superior`.
![Texto alternativo](guardar.png)
1.  `Corrida` del codigo.
![Texto alternativo](cursores13.png)
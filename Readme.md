# EDUCATATIONAL PURPOSES ONLY

Este contenido es educacional e inspirado en su autor: Idea Visuals Tech, es un extra, un programa que he diseñado para hacerlo mas facil.

[![Video de Introducción](https://img.youtube.com/vi/X0RUrIYXNaE/0.jpg)](https://www.youtube.com/watch?v=X0RUrIYXNaE)

Mis gracias a Idea Visuals Tech

Para un enfoque más eficiente, podemos usar un script basado en el calendario, ejecutado el día exacto en que quieras (por ejemplo, cada 85 días) en lugar de mantener un **LaunchDaemon** en segundo plano todo el tiempo. Esto se puede lograr con el programador de tareas de macOS, **`cron`**.

## Configuración basada en el calendario

### Paso 1: Crear el script
1. Abre **Terminal** y crea un script como antes:
   ```bash
   nano ~/clean_logic_xcode.sh
   ```
2. Añade el contenido al script:
   ```bash
   #!/bin/bash

   # Eliminar archivos de Xcode y Logic Trial
   rm -rf ~/Library/Application\ Support/.com.apple.dt.Xcode
   rm -rf ~/Library/Preferences/com.apple.logic10.plist
   sudo rm -rf /Library/Application\ Support/LogicTrial
   ```

3. Guarda y cierra el archivo (`Ctrl+O`, `Enter`, `Ctrl+X`).

4. Haz que el script sea ejecutable:
   ```bash
   chmod +x ~/clean_logic_xcode.sh
   ```

---

### Paso 2: Configurar una tarea cron

1. Abre el archivo de configuración de cron:
   ```bash
   crontab -e
   ```

2. Añade esta línea al final del archivo para programar la ejecución del script cada 85 días (por ejemplo, el día 1 de un conjunto de meses):
   ```bash
   0 0 1 */3 * /bin/bash ~/clean_logic_xcode.sh
   ```

   **Explicación del cron:**
   - `0 0 1 */3 *` -> Ejecuta a las 00:00 horas del día 1 cada 3 meses.
   - `~/clean_logic_xcode.sh` -> Ruta del script.

3. Guarda y cierra (`Ctrl+O`, `Enter`, `Ctrl+X`).

---

### Paso 3: Verificar la configuración de cron
Para verificar que tu tarea cron se haya guardado correctamente, usa:
```bash
crontab -l
```

Esto mostrará las tareas programadas en tu sistema. Deberías ver la línea que acabas de agregar.

#### ¿Por qué este método es mejor?
1. **Eficiencia:** Solo se ejecuta el día programado. El sistema no utiliza recursos adicionales innecesarios.
2. **Predecible:** La tarea está basada en el calendario y ocurre de manera precisa.
3. **Sin Daemons persistentes:** No hay necesidad de mantener un proceso en ejecución.

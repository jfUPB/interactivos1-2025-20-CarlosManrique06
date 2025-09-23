
# Evidencias de la unidad 6

<img width="576" height="362" alt="ClonarRepositoria" src="https://github.com/user-attachments/assets/31df172c-5a7b-43e6-a32e-27e43191bad4" />

Tuve que usar el github bash para clonar el repositori en el computador. Primero use el comando: git clone https://github.com/juanferfranco/entangledTest-sfi1-2025-20.git . Para clonarlo en el pc luego utilice 
el comando cd  /entangledTest-sfi1-2025-20 Para acceder al directorio, después use el code . para abrilo en visual code y el punto para abrir el directorio.

Para iniciar las pag se usa el npm install y luego npm start para correr las pag en la web.

¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?

R/

```bash
B09S113est@N00023578 MINGW64 ~/entangledTest-sfi1-2025-20 (main)
$ npm install

added 120 packages, and audited 121 packages in 4s

17 packages are looking for funding
  run `npm fund` for details
```
El terminal empezo a instalar las librerias necesarias para poder ejecutar el servidor.

¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?

<img width="757" height="377" alt="PagVacia" src="https://github.com/user-attachments/assets/1723d659-3840-4d05-b3e8-f669853c1a6b" />

R/ El mensaje esta preguntando por la direccion

Describe lo que ves inicialmente en page1 y page2 en tu navegador.

R/ <img width="386" height="276" alt="paginas" src="https://github.com/user-attachments/assets/cdca4ca1-b7b8-4a72-9c4d-16c2e3e0ac2f" />

Aparece que sincronizando datos, esperando a que se conecte a la segunda pag web.


¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?

R/ Aparece que un usuario se conecto y el id del usuario, donde se reciben los datos de ese usuario conectado.

```bash
A user connected - ID: -KLfr7wyM8QkYQ2TAAAB
Received win1update from ID: -KLfr7wyM8QkYQ2TAAAB Data: { x: 0, y: 0, width: 1920, height: 911 }

```

Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?

R/ <img width="1663" height="827" alt="Pagfuncional" src="https://github.com/user-attachments/assets/02bd5e0f-edb9-479e-8ff3-7a7d4a9bbe0c" />



Para concatenar comandos, usando ; se ejecuta primero el comando de antes del punto y coma y despues.

No es lo mismo que el &&, ya que aqui solo se ejecuta si el primero responde correctamente.

Para manejar el stderr, pondemos usar (para referenciarnos al errror), 2>/dev/null para redirijirlo aqui, y que desaparezca y no se muestre ni nada por el estilo.

Tambien, podemos redirigir todo el flujo del stdout y stderr, usando lo sigueinte &>/dev/null, que hace una combersion del stderr a stdout y luego manda todo a /dev/null.

Para poner un  proceso en segundo plano, una vez redirigido todo, podemos poner & al final para ejecutar el proceso en segundo plano.

Ademas, si agregamos al final disown, se ejecuta como proceso sin depender de ningun padre.
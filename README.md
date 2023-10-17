# Contador de 0 a 99 con Display 7 Segmentos y Multiplexacion


![Captura](https://github.com/eliascharadia/Contador-de-0-a-99-con-Display-7-Segmentos-y-Multiplexaci-n/assets/89148679/23bf2676-ac2c-4350-8398-9b714a5ac31a)


# Integrante

- Charadía Elías - 1B

## Descripción
La funcion de este proyecto es la de un contador digital de 0 a 99, con dos display de 7 segmentos controlados por multiplexacion. Se utilizan 3 botones/pulsadores para controlar los números que se muestran en los displays. Con el primer boton se incrementa en uno los números (por cada presionado al boton) y con el segundo lo mismo pero decrementa los dígitos. Luego hay un tercer boton que su función es la de resetear los displays a cero, sin importar en que numero estaba ubicado.
El último agregado es el componente switch, con el cual controlo si se van a mostrar los números primos o el contador.

## Función principal

~~~ C (lenguaje en el que esta escrito)
void loop()
{
  //Utilizo tres funciones para los botones y su funcionalidad
  //depende de lo que se requiera. Se maneja con una variable
  //incrementandola, decrementandola o reseteando la variable.
  incrementar_numeros();
  decrementar_numeros();

  //Esta funcion tiene la funcionalidad de medir la luz, si la luz es tan brillante parecido a la luz solar, los displays se apagan.
  apagar_displays_luz();
  //Parecida a la funcion anterior, esta funcion trabaja con temperatura, dependiendo si es muy alta o muy baja la temperatura
  //en el display muestro solo un segmento encendido, dando a entender que la temperatura no es apta. 
  alterar_display_segun_temperatura();


  //Manejo el funcionamiento de lo que muestran los displays
  //con el estado que recibe la entrada del switch.
  //si es HIGH muestro los numeros primos sino el contador.
  if (digitalRead(switchh) == HIGH){
    calcular_primo(cuenta);//funcion que calculo los números primos del 0 al 99
  }else{
    cuenta = cuenta;
  }
  
  //Con el número de la variable incrementada o decrementada,
  //realizo una cuenta para sacar la unidad del número de la 
  //variable y otra para sacar la decena.
  unidades = cuenta % 10;
  decenas = cuenta / 10;
  
  apagar_numero(); //Tengo que apagar el display un instante 
  //para que no se vea el número fantasma.
  
  encender_display_unidades();//Utilizo esta funcion para mostrar
  //en el display de la dereccha las unidades.
  
  apagar_numero();//Apago el display un instante.
  
  encender_display_decena();//Utilizo esta funcion para mostrar
  //en el display de la izquierda las decenas.
  
}
~~~
## MOTOR DE CORRIENT CONTINUA
Un motor de corriente continua, es un dispositivo electromecánico que convierte la energía eléctrica de corriente continua en movimiento mecánico. Son simples de usar y tienen un control de velocidad muy preciso.
-  ¿Qué es la corriente continua?

Los electrones de una corriente continua se desplazan de un punto a otro de manera constante sin cambiar su polaridad.
-  Partes de un motor CC

Los motores de corriente continua constan de dos partes principales: el rotor y el estator.
  ![image](https://github.com/eliascharadia/Contador-de-0-a-99-con-Display-7-Segmentos-y-Multiplexaci-n/assets/89148679/702e40d3-c232-448e-98ba-90e28ce02529)

El rotor es la parte giratoria del motor y generalmente contiene bobinas de alambre y el estator es la parte fija del motor el cual contiene bobinas de campo que generan un campo magnético constante.
-  Funcionamiento

Cuando se aplica una corriente continua al rotor, se crea un campo magnético que interactúa con el campo magnético del estator. Esta interacción de campos magnéticos genera un par de torsión en el rotor, lo que hace que el rotor gire y, por lo tanto, produce movimiento mecánico.
	
 Par de torsión: representa la cantidad de fuerza aplicada a un objeto en un intento de hacerlo rotar. Y se relaciona con la fuerza y la distancia desde el punto de aplicación de la fuerza al eje de giro.

-  Agregar un motor al proyecto

Se puede añadir un motor de corriente continua e indicar con los displays la velocidad a la que está girando, utilizando un pin con entrada analógica. Mientras mayor sea el número que se muestra en los displays más velocidad tendrá el giro del motor. Esto serviría para tener un control visual del movimiento del rotor del motor.

## :octocat: Link al proyecto
- [proyecto](https://www.tinkercad.com/things/dY4WhQ7JCwu-contador-de-0-a-99-con-display-7-segmentos-y-multiplexacion/editel?sharecode=UpPW-t2oktDQQsi74xRbyHPi4dNSa17naK7jZpLaioo)

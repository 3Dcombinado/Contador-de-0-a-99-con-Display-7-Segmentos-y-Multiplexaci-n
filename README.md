# Contador de 0 a 99 con Display 7 Segmentos y Multiplexacion


![Proyecto](https://github.com/eliascharadia/Contador-de-0-a-99-con-Display-7-Segmentos-y-Multiplexaci-n/assets/89148679/a2da503e-111d-4d3d-bc47-6ba1a7008d56)


# Integrante

- Charadía Elías - 1B

## Descripción
La funcion de este proyecto es la de un contador digital de 0 a 99, con dos display de 7 segmentos controlados por multiplexacion. Se utilizan 2 botones/pulsadores para controlar los números que se muestran en los displays. Con el primer boton se incrementa en uno los números (por cada presionado al boton) y con el segundo lo mismo pero decrementa los dígitos. 
Hay un agregado que es el componente switch, con el cúal controlo si se van a mostrar los números primos o el contador.
Por último se requirio sumarle dos sensores, uno de temperatura y otro de luz. A estos dos sensores se le dieron una función diferente.

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
## MOTOR DE CORRIENTE CONTINUA
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

## SENSOR DE TEMPERATURA
El TMP36 es un sensor de temperatura analógico que se utiliza para medir la temperatura ambiente. Dependiendo de la temperatura que mida, este sensor devolverá una señal de voltaje que es proporcional a los grados Celsius.
Cuanto mayor es la temperatura, mayor es la señal de voltaje generada por el sensor. El voltaje de salida puede ser interpretado para determinar la temperatura ambiente.
-	opera en un rango de -40°C a +125°C.
-	Produce una señal de voltaje analógica que puede ser directamente leída por un microcontrolador o convertida a una lectura digital.
Aplicación al proyecto:
	~~~ C (lenguaje en el que esta escrito)
	void conversion_valores_grados()
	{
	  //Leo el sensor y convierto el valor analogico a grados centigrados.
	  //con la funcion map.
	  temperatura = analogRead(SENSOR);
	  temperatura = map(temperatura, 20,358,-40,125);
	}
	
	void alterar_display_segun_temperatura()
	{
 	  //Con esta funcion capturo la temperatura y mientras sea menor a 0° o mayor a 100°
          //en el display muestro encendido solo un segmento. Despues capturo de nuevo la temperatura
 	  //y pregunto si ya está entre 0° y 100°, si se cumple la condición rompo el blucle y el programa continua normalmente
	  conversion_valores_grados();
	  while(temperatura < 0 or temperatura > 100){
	    formar_alerta();
	    conversion_valores_grados();
	    if (temperatura > 0 and temperatura < 100){
	     break; 
	    }
	  }
	    
	}
 	~~~

## FOTORESISTENCIA
Una fotoresistencia es un componente electrónico que varía su resistencia eléctrica en función de la intensidad de la luz que exista. Su resistencia disminuye cuando se expone a una mayor cantidad de luz y aumenta cuando la luz disminuye.
Para conocer la cantidad de luz que el sensor capta en cierto ambiente, se debe medir la tensión de salida del mismo. Para esto se hace uso de lo que se conoce como un divisor de tensión.
-	Divisor de tensión

es un circuito eléctrico que se utiliza para crear una salida de tensión más baja a partir de una fuente de voltaje más alta. El circuito tiene que poseer al menos dos resistencias conectadas en serie entre el voltaje de entrada y GND. 
La tensión de salida se mide desde un punto intermedio entre las dos resistencias.

![image](https://github.com/eliascharadia/Contador-de-0-a-99-con-Display-7-Segmentos-y-Multiplexaci-n/assets/89148679/4ad8c760-af6f-48d9-90a4-35502a97f5a1) 

Y la fórmula para calcular la tension de salida de un divisor de tensión es: 

	Vout = Vin * (R2 / (R1 + R2))
Para aplicar esto con una fotoresistencia, en el lugar de R1 va conectado dicho componente electrónico que actúa como una resistencia variable.	R2 tomará un valor general de 10K ohm.

Una vez aplicado el divisor de tensión, esta tensón de salida puede ser leida en una entrada analógica y apartir de ahí tien un funcionamiente similar al sensor de temperatura de arriba.

![image](https://github.com/eliascharadia/Contador-de-0-a-99-con-Display-7-Segmentos-y-Multiplexaci-n/assets/89148679/01612552-e494-4d22-9cd3-60ec7f64cc93) Fotoresistencia.


## Lógica para mostrar los números pares
- Funciónes para calcular los numeros pares.
  ~~~ C (lenguaje en el que esta escrito)
	void verificar_par(int numero)
	{
	  //Esta funcion permite saber si el número es
	  //par o impar devolviendo un booleano.
	  //True = Es par ; False = no es par.
	  if (numero % 2 == 0){
	   estado = true; 
	  }else{
	    estado = false;
	  }
	}
	
	
	void calcular_par(int numero)
	{
	  //Esta función sirve para encontrar un número par
	  //si no lo hay y lo devuelve para en este proyecto 
	  //mostrarlo en los displays.
	  verificar_par(numero);//Verifico si el numero es par
	  if (estado == true){
	    cuenta = numero;//si es par solo lo muestro.
	  }else{//si no es par, incremento en una unidad
	    //y verifico si es par. Está encerrado en un bucle
	    //para que no salga de ahi hasta que me encuentre 
	    //un numero par
	    if (subo_o_bajo == 1){
	      while(estado == false){
	        numero = numero + 1;
	        calcular_par(numero);
	      }
	    }else{
	      while(estado == false){
	        numero = numero - 1;
	        calcular_par(numero);
	      }
	    }
	  }
	}
 	~~~
  Primero hay que saber si el número que se necesita mostrar en los displays es par o impar. Para eso sirve la función "verificar par", la cual recibe como parametro una variable de tipo entero
  a la que se hace el procedimiento.
  La función "calcular par" se puede decir que es la principal. El primer paso de esta funcion seria aplicar el tratamiento de la función anterior con el parametro que se le envio a esta nueva función.
  Después de la verificación, se analiza si es par o impar. Si es impar se va a buscar el número mas proximo PAR y lo devuelve, si ya de por si es par no se somete a este procedimiento.
 
## :octocat: Link al proyecto
- [proyecto](https://www.tinkercad.com/things/2hc4EQ8or8j-2do-parcial-1b-elias-charadia/editel?sharecode=tz5tiXZC_ijjYl3a7FwzIRzA8Sweb0hnFXltIoTnDr0)

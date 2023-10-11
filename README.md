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

## :warning: Link al proyecto
- [proyecto](https://www.tinkercad.com/things/0SVh8mW4Zjm-contador-de-0-a-99-con-display-7-segmentos-y-multiplexacion/editel?sharecode=niWuMdXmHFZatJbscutm-X0j1dP26iuFYto8ctSO4mA)

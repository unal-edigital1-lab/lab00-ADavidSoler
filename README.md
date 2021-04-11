# lab01- sumador 
laboratorio 01 introducción a HDL

En esta plantilla debe adicionar la documentación del laboratorio

* Andres David Rodríguez Soler

##Parte 1

Para el primer laboratorio de Electrónica digital 1 se procede a realizar un sumador que consiste en tres entradas de 1 bit que serán adicionadas para así obtener una salida. Para este procedimiento se hace uso de la herramienta Quartus de Intel. Aquí se crea un proyecto, el cual corresponderá al sumador. En este proyecto se introduce el código funcional del sumador:
```
module sum1bcc_primitive (A, B, Ci,Cout,S);

  input  A;
  input  B;
  input  Ci;
  output Cout;
  output S;


  wire a_ab;
  wire x_ab;
  wire cout_t;

  and(a_ab,A,B);
  xor(x_ab,A,B);

  xor(S,x_ab,Ci);
  and(cout_t,x_ab,Ci);

  or (Cout,cout_t,a_ab);

endmodule
```
Después se realiza la compilación de este. Con esto se obtiene que el código es correcto y no arroja ningún error. 

 
 ![1](https://user-images.githubusercontent.com/80412854/114294217-a889ae80-9a62-11eb-9dae-97a768e53a1d.png)



Con el código listo y la compilación hecha y satisfactoria, se procede a realizar la simulacion en Altera, un programa adicional que ayuda con la visualización de los datos de Quartus. Para esto, se realiza la compilación de RTL. 

Con una compilación exitosa, se obtiene una nueva ventana del programa, así como tambien una ventana de visualización de ondas. 

  ![2](https://user-images.githubusercontent.com/80412854/114294222-b5a69d80-9a62-11eb-826f-7f2509a47646.png)


En esta ventana de ondas se realiza la prueba del código mediante las ondas o señales. Se fuerza el valor de cada una de las entradas. Ya que son tres, existen ocho posibles combinaciones para realizar la suma, es decir, se modificaron los valores de las tres entradas un total de 8 veces. Esto con el fin de comprobar el buen funcionamiento del código. 

 
 ![3](https://user-images.githubusercontent.com/80412854/114294223-b8a18e00-9a62-11eb-9672-da15f2fda140.png)




Con las ondas se comprueba que el sumador hace el procedimiento de manera correcta. 


##Parte 2

Para la segunda parte de este primer laboratorio, se requiere realizar nuevamente un sumador, pero esta vez de 4 bits. Para lograr esto, se hace uso del código anterior, el del sumador de 1 bit, ya que a partir de este, y de manera escalonada, se puede lograr esta suma. Para este nuevo proyecto, se crea un nuevo archivo, y se introduce el siguiente código:
```
module sum4bcc (xi, yi,co,zi);

  input [3 :0] xi;
  input [3 :0] yi;
  output co;
  output [3 :0] zi;

  wire c1,c2,c3;
  sum1bcc s0 (.A(xi[0]), .B(yi[0]), .Ci(0),  .Cout(c1) ,.S(zi[0]));
  sum1bcc s1 (.A(xi[1]), .B(yi[1]), .Ci(c1), .Cout(c2) ,.S(zi[1]));
  sum1bcc s2 (.A(xi[2]), .B(yi[2]), .Ci(c2), .Cout(c3) ,.S(zi[2]));
  sum1bcc s3 (.A(xi[3]), .B(yi[3]), .Ci(c3), .Cout(co) ,.S(zi[3]));


endmodule
```
Como se puede ver, este código usa el anterior de 1 bit, por lo que se hace necesario incluirlo en el nuevo proyecto. Así, se queda con dos códigos, uno como función del otro. 

  ![4](https://user-images.githubusercontent.com/80412854/114294226-c1925f80-9a62-11eb-9a66-6dc8dd212a27.png)


Ahora, la idea con este nuevo proyecto, es hacer uso de una nueva herramienta, la cual es una tarjeta de procesamiento Intel FPGA. Para hacer uso de esta en combinación con el computador, se instala un driver para que la comunicación entre los dos dispositivos sea efectiva. Adicionalmente, en el programa Quartus, se le indica en este proyecto que se trabajará con este tipo de tarjeta. En este paso tambien se debe indicar el modelo de la tarjeta, la cual en este caso es una de la serie Cyclone IV.

Luego de configurar el computador y el programa, ya se puede empezar a programar esta tarjeta. En este paso, se realiza la planeación de los pines. Para este caso, se tienen 8 entradas, o tambien dos números de 4 bits. Es decir, se deben programar 8 pines, los cuales en este caso serán 8 switchs de los que dispone la tarjeta, para ser las entradas. Adicionalmente, se debe contar con 4 salidas, las cuales corresponden a los 4 bits del número resultante de la suma. Estas 4 salidas tendran pines asignados a 4 leds, los cuales se prenderán o apagarán de acuerdo al resultado, si corresponde a un 1 o a un 0.

 
 ![5](https://user-images.githubusercontent.com/80412854/114294227-c6571380-9a62-11eb-8260-b9c6e7a25ea5.png)




Luego de hacer la configuración de los pines, se puede pasar esta informacion a la tarjeta, por lo que se abre el asistente Programmer, el cual tiene como función la comunicación con la tarjeta desde el programa Quartus. 

 
 ![6](https://user-images.githubusercontent.com/80412854/114294234-cc4cf480-9a62-11eb-837d-00cf6ae10bc9.png)



Se puede notar que el USB-Blaster esta activo, esto significa que el programa reconoce la tarjeta a través del puerto. Al hacer click en Start, se envia la información previamente descrita a la tarjeta, arrojando un envío exitoso. 

Ahora, se procede a hacer uso de la tarjeta para comprobar su funcionamiento. 

En la tarjeta se tienen los 8 switchs, los cuales al alternarlos indican un valor de 1 o 0. De esta forma, se puede realizar la suma de números en formato binario.

Al hacer uso de la tarjeta, se nota que el orden de los switch esta invertido, sin embargo, la suma es correcta y los leds se prenden para indicar un 0 y se apagan para indicar un 1. Con varias pruebas de sumas se da un visto bueno al funcionamiento. 

 
![WhatsApp Image 2021-04-10 at 20 05 37](https://user-images.githubusercontent.com/80412854/114294242-d7078980-9a62-11eb-9be4-6c22420e1f84.jpeg)
![WhatsApp Image 2021-04-10 at 20 06 26](https://user-images.githubusercontent.com/80412854/114294243-d969e380-9a62-11eb-852c-e04e070d05b9.jpeg)

 


 
 


 

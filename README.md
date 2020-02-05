# ARSW-LAB2

## Part I - Before finishing class

### Thread control with wait/notify. Producer/consumer

**Check the operation of the program and run it. While this occurs, run jVisualVM and check the CPU consumption of the corresponding process. Why is this consumption? Which is the responsible class?** 

![](/img/Imagen1.png)

* El consumo de CPU es elevado porque el subproceso de la clase **Consumer** está constantemente comprobando en la cola los nuevos números para consumir.

**Make the necessary adjustments so that the solution uses the CPU more efficiently, taking into account that - for now - production is slow and consumption is fast. Verify with JVisualVM that the CPU consumption is reduced.** 

![](/img/Imagen2.png)

**Make the producer now produce very fast, and the consumer consumes slow. Taking into account that the producer knows a Stock limit (how many elements he should have, at most in the queue), make that limit be respected. Review the API of the collection used as a queue to see how to ensure that this limit is not exceeded. Verify that, by setting a small limit for the 'stock', there is no high CPU consumption or errors.**

![img](https://github.com/fernando-b15/CNYT-Actividad-Esfera/blob/master/lab2-3.PNG)

## Past II - Synchronization and Dead-Locks.

- Review the code and identify how the functionality indicated above was implemented. Given the intention of the game, an invariant should be that the sum of the life points of all players is always the same (of course, in an instant of time in which a time increase / reduction operation is not in process ). For this case, for N players, what should this value be?
100*N

- Run the application and verify how the ‘pause and check’ option works. Is the invariant fulfilled?
Cuando inicia la aplicación por primera vez, podemos notar que la invariante no se cumple, ya que cada vez que hace click en el botón “Pause and Check”, da diferentes valores en la suma del total de la vida de todos los jugadores.

- Check the operation again (click the button many times). Is the invariant fulfilled or not ?.
No, la suma de la vida total aun no es consistente. 

- Identify possible critical regions in regards to the fight of the immortals. Implement a blocking strategy that avoids race conditions. Remember that if you need to use two or more ‘locks’ simultaneously, you can use nested synchronized blocks.
Al no sincronizarse la vida de los jugadores.

- An annoying element for the simulation is that at a certain point in it there are few living 'immortals' making failed fights with 'immortals' already dead. It is necessary to suppress the immortal dead of the simulation as they die. 
  1. Analyzing the simulation operation scheme, could this create a race condition? Implement the functionality, run the simulation and see what problem arises when there are many 'immortals' in it. 
Si, ya que todos los jugadores muertos siguen peleando y intentan acceder a recursos innecesariamente, esto se debe al “while(true)” y lo arreglamos al hacer que dejaran de pelear cuando la vida sea cero.
  
  2. Correct the previous problem WITHOUT using synchronization, since making access to the shared list of immortals sequential would make simulation extremely slow.
  

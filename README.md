# BIP-39


### Generacion de mnemonic
**Paso 1  Decidir el numero de palabras se quiere generar**

> Pueden ser  12, 15, 18, 21 o 24 palabras.

 **Paso 2 Calcular la entropia en un rango de 128 a 256 bits**

> Se van a sacar 12 palabras ( para este ejemplo). Es por eso que a nivel de bits se genera una entropia de 128 y se le suman 4 mas para que sean 132 numero que es multiplo de 11(porque se divide en grupos de 11 a nivel de bits) y si dividimos 132 /11 = 12 (Palabras).Posteriormente se necesita separar en grupos de 11 bits ya que la lista es de
> 2 a la 11 que es igual a 2048. Si ponermos once unos en formato binario 1111 1111 1111 11 lo maximo 
> que pueden representar es 2047 cada grupo de 11 representara una palabra y es asi como se generan las 12 palabras

**Link a las 2048 palabras github en ingles**

*https://github.com/bitcoin/bips/blob/master/bip-0039/english.txt*

**Paso 3 Calcular el checksum( osea SHA-256 )**

> Se saca el hash de la entropia en este caso de 128 bit (12 palabras) y para llegar a poder hace grupos de 11 y sacar 12 palabras pues se requieren
> 4 bits extra osea quedaria en 132. Entonces recapitulando sacamos el hash de la entropia y agarramos los 4 primeros bits.(Recordar que cada caracter hex son 4 bits)
**Paso 4 Concatenar los primeros bites del hash sha256 tambien llamado checksum***
> Se concatenan los primero bytes dependiendo de la longitud de la entropia para despues asociar cada 11 bits con su respectiva palabra de la lista de 2048

**Ejemplo con Bash y Python**

**python3**

`entr='0c1e24e5917779d297e14d45f14e1a1a'` *Entropia en hexadecimal 32 bytes multiplicado por 4(de cada numero hex) nos da 128 bits Nota: No olvides que el 0 vale 0000 en bits el del inicio 0c*

`print(bin(int(entr,16)))`  *Convertimos de hex a enteros despues a binario lo cual nos da 

`00001100000111100010010011100101100100010111011101111001110100101001011111100001010011010100010111110001010011100001101000011010`

`echo 00001100000111100010010011100101100100010111011101111001110100101001011111100001010011010100010111110001010011100001101000011010 | shasum -a 256 -0`

> El hash que genera ***7***6e57a90f93135e97ce700a9e79196ba46315d65e696d0a4518270a8de3e80e4 osea ***0111***
> 
> El anterior comando saca la chechsum de nuestra entropia y posteriormente le sacaremos los primero 4 bits al hash que se genero tambien llamado checksum para posteriormente ponerlos al final de la entropia dando un multiplo de 11 para poder formar para este caso las 12 palabras.
> 
> 00001100000 11110001001 00111001011 00100010111 01110111100 11101001010 01011111100 00101001101 01000101111 10001010011 10000110100 0011010***0111***
> 
>  Recuerda que esto es index 0 entonces para buscar en la lista lo que te salga al pasarlo a decimal sumale uno.
>  Las 12 palabras que corresponden a esos numeros son: 

***army van defense carry jealous true garbage claim echo media make crunch***














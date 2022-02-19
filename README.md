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

**Ejemplo con Bash y Python**

*python3*

`entr='0c1e24e5917779d297e14d45f14e1a1a'` *Entropia en hexadecimal 32 bytes multiplicado por 4(de cada numero hex) nos da 128 bits*

`print(bin(int(entr,16)))`  *Convertimos de hex a enteros despues a binario lo cual nos da 1100000111100010010011100101100100010111011101111001110100101001011111100001010011010100010111110001010011100001101000011010*

`echo 1100000111100010010011100101100100010111011101111001110100101001011111100001010011010100010111110001010011100001101000011010 | shasum -a 256 -0`

> El anterior comando saca la chechsum de nuestra entropia y posteriormente le sacaremos los primero 4 bits.
> 
> **6**16462856361e566d20e33fc18e3ae03578d678135e7b6007511c62418f29a31
> 















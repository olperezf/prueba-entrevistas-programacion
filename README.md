# Ejercicios - Pruebas de entrevista de programación
---
Ejercicios y Pruebas reales de entrevistas basados en las páginas de challenge de programación más conocidas como: 

Coderbyte: es una solución de pruebas previas al empleo basada en la nube que ayuda a las empresas a realizar evaluaciones de programación para puestos técnicos.

Codewar: (Wikipedia) es una comunidad educativa de programación de sistemas. En la plataforma, los desarrolladores de software participan en desafíos de programación conocidos como kata. Estos ejercicios entrenan un rango de habilidades en una variedad de lenguajes de programación y se completan dentro de un ambiente de desarrollo integrado en línea, en el que los usuarios tienen la posibilidad de ganar rangos y honor

Mi perfil en Codewar:   
https://www.codewars.com/users/pomer/completed

TestDome: pruebas automatizadas de habilidades previas al empleo. Para probar si un candidato será bueno en el trabajo, la solución ofrece una muestra del trabajo real.

---

Correo: Dependiendo de la empresa a veces mandan a resolver los challenges por la plataforma de coderbyte, por sus propias plataformas, o mandan un correo con el problema para resolverlo en la plataforma local.

Para ver la solución del ejercicio hacer Click en la pregunta.

El siguiente ejercicio fué enviado por correo, para resolverlo localmente:

## Ejercicio #1:
    Plataforma: Correo
    Lenguaje: Ruby

<details>
    <summary>Sin usar el built-in method de ruby que se llama "rotate":
Dado un arreglo A de N índices [A(0), A(1), A(2), ..., A(N-1), A(N)] se dice que se "rota" una vez quedando A(K=1)=[A(N), A(0), A(1), A(2), ..., A(N-1)], esta rotación puede ocurrir K veces dando como resultado un arreglo final B.</summary> 
    
a) Desarrolle un método que dado un array A y una cantidad K, rote el array K veces dando un array B. Ejemplo:

    A = [1,2,3,4,5]
    K = 3
    B = rotate(A,K)
    => [3,4,5,1,2]

Solución:

    # Método utilizando un array
    def rotate(array,k)
        k.times do # numero de veces que se va rotando los elementos
            last_element = array[-1]# rescato el ultimo elemento
             array.pop()# elimino el ultimo elemento del array
             array.insert(0, last_element)# inserto el ultimo elemento en la primera posición del array  
        end
        return array
    end
    
    # Método de rotate version 2 utilizando 2 arrays
    def rotate_v2(k,array_a)
       array_b = []
       k.times do
           for key in 0..(array_a.length-1) do  # for que itera n veces depende de la longitud del array    
               array_b[key] = array_a[key-1]  # va rodando los elementos copiandolo en el array_b
           end
           array_a.replace(array_b) # copia el array_b al array_a para que el siguiente ciclo del for tome los 
       end                          # ultimos cambios del array_b
       return array_b
    end



b) Qué pasa si llamo al método con K = 500000000000000001 para el ejemplo anterior? Como puedo hacer que sea calculado en menos de 1 segundo?

Como se podrá observar en el enunciado arriba, se implementó 2 métodos de rotate: 1)rotate y 2)rotate_v2.

Para el primer método rotate  llamando k = 500000000000000001 ( 5×10¹⁷+ 1) obtuve como resultado:Aprox: 25 siglos, Para llegar a ese resultado se realizó la siguiente secuencia de pruebas:

    para k = 5000000 tardó 1 segundo
    para k = 50000000 tardó 8 segundos
    para k = 500000000 tardó 80 segundos
    para k = 5000000000 tardó 800 segundos, 
    ahora como se podrá observar se esta realizando una multiplicacion x 10 en cada secuencia de k 
    dando como resultados la multiplicacion de segundos, y extrapolando para k = 5000000000000000001 
    tarda aproximadamente 25 siglos en resolver este proceso. 
    (tener en cuenta también el procesador de la máquina para que pueda dar estos resultados)


    para el método rotate_v2 con k = 500000000000000001 obtuve como resultado 190 siglos, igual como en el método anterior se realizó la secuencia a partir de:
    para k = 5000000 tardó 6 segundo
    para k = 50000000 tardó 60 segundos
    para k = 500000000 tardó 600 segundos (10 minutos) y extrapolando para k = 5000000000000000001 tarda aproximadamente 190 siglos en resolver este proceso.

Hasta ahora se puede evaluar cual es el algoritmo más eficiente y rápido en cuanto a procesar la informacion, que en este caso es el primer método rotate.


Solución para que pueda calcular el proceso en menos de un segundo:

    def rotate_v5(array,k)
        # Línea de código que hace que calcule en menos de un segundo
        k = k % array.length # hay que dividir el k entre la longitud del array y da un resto, 
                             # este resto es la posicion que se rotara el elemento dentro del array, 
                             # ya que el cociente es la parte exacta que siempre estara en la misma posicion.
        k.times do # numero de veces que se va rotando los elementos
            last_element = array[-1] # rescato el ultimo elemento
             array.pop() # elimino el ultimo elemento del array
             array.insert(0, last_element) # inserto el ultimo elemento en la primera posición del array  
        end
        return array
    end
    
</details>
    
    
## Ejercicio #2:
    Plataforma: TestDome
    Lenguaje: Ruby
    
<details>
    <summary>Implementar la función sort_by_price_ascending, which: 
- Acepta una cadena en formato JSON.
- Ordena los artículos por precio en orden ascendente.
- Si dos productos tienen el mismo precio, los ordena por su nombre en orden alfabético.
- Devuelve una cadena en formato JSON que es equivalente a la del formato de entrada.</summary>
    
Solución:

    require 'json'
    
    def sort_by_price_ascending(json_string)
        return (JSON[json_string].sort_by{ |hash| hash['price'].to_s + hash['name'].to_s }).to_json
    end
    
    puts sort_by_price_ascending('[{"name":"eggs","price":1},{"name":"coffe","price":1},{"name":"korn","price":9.99},{"name":"rice","price":4.04},{"name":"banana","price":1},{"name":"platano","price":4.04}]')
    
Salida en consola:

    [{"name":"banana","price":1},{"name":"coffe","price":1},{"name":"eggs","price":1},{"name":"platano","price":4.04},{"name":"rice","price":4.04},{"name":"korn","price":9.99}]
    
Análisis:

require 'json' : Requerimos del método require para invocar la librería 'json'   
JSON[json_string] : Genera un hash a partir del json.    
sort_by{ |hash| hash['price'].to_s + hash['name'].to_s } : Utilizamos el método sort_by para ordenar; primero ordena por nombre alfabéticamente, y luego por el precio.  
to_json : Convierte el hash en formato json
    
</details>


## Ejercicio #3:
    Plataforma: TestDome
    Lenguaje: Ruby
    
<details>
    <summary> Una aplicación requiere que diferentes formatos de fecha se conviertan en un formato de fecha común.    
Implemente la función transform_date_format que acepta una lista de fechas como cadenas y devuelve
una nueva lista de cadenas que representan fechas en el formato AAAAMMDD. Todas las fechas de ingreso serán válidas,
pero solo aquellas que tengan los siguientes formatos: AAAA / MM / DD, DD / MM / AAAA y MM-DD-AAAA deben ser
incluido en la lista devuelta, donde AAAA, MM y DD son números que representan año, mes y día, respectivamente.

Ejemplo:

    transform_date_format(["2010/02/20","19/12/2016","11-18-2012","20130720"]) 
    debería retornar una lista:  ["20100220","20161219","20121118"]. 
</summary>

Solución:

    require 'date'
    
    def transform_date_format(dates)
       result =[]
       for key in 0..(dates.length-1) do
         result.push(Date.strptime(dates[key], "%m-%d-%Y").strftime('%Y%m%d')) if dates[key].include?"-"
         result.push(Date.parse(dates[key]).strftime('%Y%m%d')) if dates[key].include?"/"
       end 
       return result
    end  

    p transform_date_format(["2010/02/20", "19/12/2016", "11-18-2012", "20130720"])
    
Salida consola:

    ["20100220", "20161219", "20121118"]
    
Análisis:  

Date.strptime : es un método de clase DateTime que analiza la representación dada de fecha y hora con la plantilla dada.    
strftime('%Y%m%d') : es un método de clase de tiempo que devuelve el formato.   
Date.parse(dates[key]) : parsea  formatos de fechas incluyendo yyyy/mm/dd, dd/mm/yyyy.   
Pero este tipo de formato: mm-dd-yyyy, no lo reconoce
    
</details>


## Ejercicio #4:
    Plataforma: Coderbyte
    Lenguaje: Ruby
    
<details>
    <summary> En el archivo Ruby, escriba un programa para realizar una solicitud GET en la ruta https://coderbyte.com/api/challenges/json/age-counting
 que contiene una clave de datos y el valor es una cadena que contiene elementos en el formato: key = STRING, age = INTEGER. Tu objetivo es contar cómo
 Existen muchos elementos que tienen una edad igual o superior a 50, e imprime este valor final

Ejemplo:

    {"data":"key=IAfpK, age=58, key=WNVdi, age=64, key=jp9zt, age=47}
    Salida:
           2 
        
</summary>

Solución:

    require 'net/http'
    require 'json'
    def age_counting
      uri = URI('https://coderbyte.com/api/challenges/json/age-counting')
      response = Net::HTTP.get(uri)
      return  Hash[*JSON.parse(response)["data"].scan(/\b(?!age\b)\b(?!key\b)\w+/)].select{|k,v| v.to_i >= 50}.size
    end

    
Salida consola:

     => 128   -> Registros
    
Análisis:  

require 'net/http' : Proporciona una biblioteca rica que se puede utilizar para crear agentes de usuario HTTP   
require 'json' : JSON (JavaScript Object Notation) Es un formato de intercambio de datos ligero 
URI('https://coderbyte.com/api/challenges/json/age-counting') : URI es un módulo que proporciona clases para manejar identificadores uniformes de recursos. 
Para esta url URI lo convierte asi:
    
        #<URI::HTTPS https://coderbyte.com/api/challenges/json/age-counting>

response = Net::HTTP.get(uri) : Obtenemos los datos de la página que estamos consultando; en esta url 'https://coderbyte.com/api/challenges/json/age-counting'
obtenemos 300 registros, para nuestro ejemplo voy a tomar una muestra de 20 registros que obtenemos del response:
    
    "{\"data\":\"key=IAfpK, age=58, key=WNVdi, age=64, key=jp9zt, age=47, key=0Sr4C, age=68, key=CGEqo, age=76, key=IxKVQ, age=79, key=eD221, age=29, 
     key=XZbHV, age=32, key=k1SN5, age=88, key=4SCsU, age=65, key=q3kG6, age=33, key=MGQpf, age=13, key=Kj6xW, age=14, key=tg2VM, age=30, key=WSnCU,
     age=24, key=f1Vvz, age=46, key=dOS7A, age=72, key=tDojg, age=82, key=nZyJA, age=48, key=R8JTk, age=29\"}"

JSON.parse(response) : Parseamos los resgistros quedando un hash.
    
    {"data"=>"key=IAfpK, age=58, key=WNVdi, age=64, key=jp9zt, age=47, key=0Sr4C, age=68, key=CGEqo, age=76, key=IxKVQ, age=79, key=eD221, age=29, key=XZbHV,
    age=32, key=k1SN5, age=88, key=4SCsU, age=65, key=q3kG6, age=33, key=MGQpf, age=13, key=Kj6xW, age=14, key=tg2VM, age=30, key=WSnCU, age=24,
    key=f1Vvz, age=46, key=dOS7A, age=72, key=tDojg, age=82, key=nZyJA, age=48, key=R8JTk, age=29"}

JSON.parse(response)["data"] : Obtendremos el value string.
    
    "key=IAfpK, age=58, key=WNVdi, age=64, key=jp9zt, age=47, key=0Sr4C, age=68, key=CGEqo, age=76, key=IxKVQ, age=79, key=eD221, age=29, key=XZbHV, 
    age=32, key=k1SN5, age=88, key=4SCsU, age=65, key=q3kG6, age=33, key=MGQpf, age=13, key=Kj6xW, age=14, key=tg2VM, age=30, key=WSnCU, age=24,
    key=f1Vvz, age=46, key=dOS7A, age=72, key=tDojg, age=82, key=nZyJA, age=48, key=R8JTk, age=29"
    
JSON.parse(response)["data"].scan(/\b(?!age\b)\b(?!key\b)\w+/) : Escaneamos toda la cadena convirtiendola en un array eliminando las palabras "key", "age", la coma "," y el igual "=", separando todo en elementos.
    
    ["IAfpK", "58", "WNVdi", "64", "jp9zt", "47", "0Sr4C", "68", "CGEqo", "76", "IxKVQ", "79", "eD221", "29", "XZbHV", "32", "k1SN5", "88", 
    "4SCsU", "65", "q3kG6", "33", "MGQpf", "13", "Kj6xW", "14", "tg2VM", "30", "WSnCU", "24", "f1Vvz", "46", "dOS7A", "72", "tDojg", "82", 
    "nZyJA", "48", "R8JTk", "29"]

Hash[*JSON.parse(response)["data"].scan(/\b(?!age\b)\b(?!key\b)\w+/)] : Convertimos todo en hash.
    
    {"IAfpK"=>"58", "WNVdi"=>"64", "jp9zt"=>"47", "0Sr4C"=>"68", "CGEqo"=>"76", "IxKVQ"=>"79", "eD221"=>"29", "XZbHV"=>"32", "k1SN5"=>"88", 
    "4SCsU"=>"65", "q3kG6"=>"33", "MGQpf"=>"13", "Kj6xW"=>"14", "tg2VM"=>"30", "WSnCU"=>"24", "f1Vvz"=>"46", "dOS7A"=>"72", "tDojg"=>"82", 
    "nZyJA"=>"48", "R8JTk"=>"29"}

Hash[*JSON.parse(response)["data"].scan(/\b(?!age\b)\b(?!key\b)\w+/)].select{|k,v| v.to_i >= 50} : Seleccionamos los registros que sean igual o mayor que 50
    
    {"IAfpK"=>"58", "WNVdi"=>"64", "0Sr4C"=>"68", "CGEqo"=>"76", "IxKVQ"=>"79", "k1SN5"=>"88", "4SCsU"=>"65", "dOS7A"=>"72", "tDojg"=>"82"}

Hash[*JSON.parse(response)["data"].scan(/\b(?!age\b)\b(?!key\b)\w+/)].select{|k,v| v.to_i >= 50}.size : Muestra la cantidad de registros que tienen la edad
igual o mayor que 50.
    
    => 9 
    
</details>
    
## Ejercicio #5:
    Plataforma: Coderbyte
    Lenguaje: Ruby
    
<details>
    <summary> Haga que la función MathChallenge(num) tome el parámetro num que se está pasando y determine el número de dos dígitos más grande
        dentro del número entero. Por ejemplo: si num es 4759472, entonces su programa debería devolver 94 porque ese es el más grande
        número de dos dígitos. La entrada siempre contendrá al menos dos dígitos positivos.

Ejemplo:

    input: 453857
    Output: 85

    input: 363223311
    Output: 63 
        
</summary>    

Solución:

    def MathChallenge(num)
      return num.to_s.scan(/./).each_cons(2).to_a.map(&:join).max.to_i
    end

    MathChallenge(13575396797)
    
Salida consola:

     => 97 
    
Análisis:    

num.to_s.scan(/./) : Convertimos el numero en String para luego convertir cada numero en elemento de un array por ejemplo:
    
    ["1", "3", "5", "7", "5", "3", "9", "6", "7", "9", "7"]

A continuación utilizamos .each_cons(2).to_a : es un método  que itera para N (en nuestro caso N es = 2) elementos consecutivos 
comenzando desde cada elemento cada vez, convirtiendo cada elemento en un arreglo:
    
    [["1", "3"], ["3", "5"], ["5", "7"], ["7", "5"], ["5", "3"], ["3", "9"], ["9", "6"], ["6", "7"], ["7", "9"], ["9", "7"]]
    
map(&:join) : Hacemos un join por cada elemento:
    
    ["13", "35", "57", "75", "53", "39", "96", "67", "79", "97"] 
    
Y finalizamos con max.to_i : buscamos el numero mayor del arreglo y lo convertimos en entero:
    
    97
     

</details>    

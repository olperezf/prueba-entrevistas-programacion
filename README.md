# Ejercicios - Pruebas de entrevista de programación
---
Ejercicios y Pruebas reales de entrevistas basados en las páginas de challenge de programación más conocidas como: 

Coderbyte: es una solución de pruebas previas al empleo basada en la nube que ayuda a las empresas a realizar evaluaciones de programación para puestos técnicos.

Codewar: (Wikipedia) es una comunidad educativa de programación de sistemas. En la plataforma, los desarrolladores de software participan en desafíos de programación conocidos como kata. Estos ejercicios entrenan un rango de habilidades en una variedad de lenguajes de programación y se completan dentro de un ambiente de desarrollo integrado en línea, en el que los usuarios tienen la posibilidad de ganar rangos y honor

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



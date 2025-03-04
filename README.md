# Test
Parte 2 test
# Problema 1:Dada un arreglo de enteros, devuelva los 
# índices de los dos números de modo que se sume un número específico.

def indices(numeros, suma_objetivo):
    """
    Devuelve los índices de dos números en el array que suman el valor objetivo.
    
    Argumentos(input)
        numeros: Lista de enteros
        suma objetivo: Suma objetivo
    
    Retorno(output):
        Lista con los dos índices cuya suma es igual al target
    """
    # Diccionario para almacenar el valor y su índice
    diccionario_numeros = {}
    
    for i, numero in enumerate(numeros):
        # Calculamos el complemento necesario para alcanzar la suma objetivo
        complemento = suma_objetivo  - numero
        
        # Si el complemento ya está en el diccionario, hemos encontrado la solución
        if complemento in diccionario_numeros:
            return [diccionario_numeros[complemento], i]
        
        # Guardamos el número actual y su índice
        diccionario_numeros[numero] = i
    
    # No debería llegar aquí si se garantiza una solución
    return None


# Ejemplo de uso:
numeros = [2,7,11,15]
suma_objetivo = 9
print(f"Índices de los números que suman {suma_objetivo }: {indices(numeros, suma_objetivo )}")


#########################################################################################################


# Problema 2: Un sistema de información cuenta con tres agentes (A, B y C) 
# cada agente cumple con dos funcionalidades

class Agente:
    #Método base para obtener la media
    def getMedia(self, numeros):
        pass
    
    #Método base para generar una escalera
    def getStaircase(self, n):
        pass

#Agente A
"""
a.Calcula la media aritmética (promedio)
Argumentos(input): numeros: Lista de números reales
Retornos(output): Número real que representa la media aritmética
b. Genera una escalera alineada a la derecha
Argumentos(input): n: Tamaño de la escalera
Retornos(output): Cadena que representa la escalera
"""
class AgenteA(Agente):
    def getMedia(self, numeros):
        if not numeros:
            return 0
        return sum(numeros) / len(numeros)
    
    def getStaircase(self, n):
        if n <= 0 or n >= 100:
            return "Valor de n fuera del rango permitido (0 < n < 100)"
        resultado = []
        for i in range(n):
            # Espacios a la izquierda + símbolos #
            resultado.append(' ' * (n - i - 1) + '#' * (i + 1))
        
        return '\n'.join(resultado)


#Agente B
"""
a.Calcula la media armónica
Argumentos(input): numeros: Lista de números reales
Retornos(output): Número real que representa la media armónica
b. Genera una escalera alineada a la izquierda
Argumentos(input): n: Tamaño de la escalera
Retornos(output): Cadena que representa la escalera
"""
class AgenteB(Agente):
    def getMedia(self, numeros):
        if not numeros:
            return 0
        # Verificar que no haya ceros en la lista
        if 0 in numeros:
            raise ValueError("La media armónica no está definida cuando hay ceros en los datos")
        
        suma_inversos = sum(1/x for x in numeros)
        return len(numeros) / suma_inversos
    
    def getStaircase(self, n):
        if n <= 0 or n >= 100:
            return "Valor de n fuera del rango permitido (0 < n < 100)"
        resultado = []
        for i in range(n):
            # Símbolos # sin espacios a la izquierda
            resultado.append('#' * (i + 1))
        
        return '\n'.join(resultado)

#Agente C
"""
a. Calcula la mediana
Argumentos(input): numeros: Lista de números reales
Retornos(output): Número real que representa la mediana
b. Genera una escalera centrada
Argumentos(input): n: Tamaño de la escalera
Retornos(output): Cadena que representa la escalera
"""

class AgenteC(Agente):
    def getMedia(self, numeros):
        if not numeros:
            return 0
        # Ordenar la lista
        ordenados = sorted(numeros)
        longitud = len(ordenados)
        # Si la longitud es impar
        if longitud % 2 == 1:
            return ordenados[longitud // 2]
        # Si la longitud es par
        else:
            idx_medio1 = longitud // 2 - 1
            idx_medio2 = longitud // 2
            return (ordenados[idx_medio1] + ordenados[idx_medio2]) / 2
    
    def getStaircase(self, n):
        if n <= 0 or n >= 100:
            return "Valor de n fuera del rango permitido (0 < n < 100)"
        resultado = []
        # Primera mitad (descendente)
        centro_max = n + (n-1)*2  # El ancho máximo en el centro
        for i in range(n):
            num_caracteres = n + i*2
            espacios = (centro_max - num_caracteres) // 2
            resultado.append(' ' * espacios + '#' * num_caracteres)
        # Patrón descendente (sin incluir la línea central)
        for i in range(n-2, -1, -1):
            num_caracteres = n + i*2
            espacios = (centro_max - num_caracteres) // 2
            resultado.append(' ' * espacios + '#' * num_caracteres)
        return '\n'.join(resultado)


# Ejemplos de uso

# Crear instancias de los agentes
agente_a = AgenteA()
agente_b = AgenteB()
agente_c = AgenteC()

# Ejemplo para getMedia
numeros_ejemplo = [1, 2, 3, 4, 5]
print(f"Media aritmética (Agente A): {agente_a.getMedia(numeros_ejemplo)}")
print(f"Media armónica (Agente B): {agente_b.getMedia(numeros_ejemplo)}")
print(f"Mediana (Agente C): {agente_c.getMedia(numeros_ejemplo)}")

# Ejemplo para getStaircase
n_ejemplo = 4
print("\nEscalera Agente A (n=4):")
print(agente_a.getStaircase(n_ejemplo))

print("\nEscalera Agente B (n=4):")
print(agente_b.getStaircase(n_ejemplo))

print("\nEscalera Agente C (n=4):")
print(agente_c.getStaircase(n_ejemplo))

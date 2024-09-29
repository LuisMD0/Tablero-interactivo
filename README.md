# Tablero-interactivo

import streamlit as st

# Título y descripción general
st.set_page_config(page_title="Tablero de Ejercicios Interactivo", page_icon="📊", layout="centered")
st.title("📚 Tablero Interactivo de Ejercicios en Python")
st.write("Organizado por: Luis Alejandro Mejia Duran - 3°D")

# Crear pestañas para cada función
tabs = st.tabs(["👋 Saludo", "➕ Suma de Números", "📐 Área del Triángulo", "💸 Calculadora de Descuento", 
                "🔢 Suma de Lista", "🛒 Valores Predeterminados", "🔍 Pares e Impares", 
                "✖️ Multiplicación con *args", "📝 Información Personal", "🧮 Calculadora Flexible"])

# 1. Saludo simple
def ejercicio_saludo():
    if 'name' not in st.session_state:
        st.session_state.name = ""
    if 'saludos' not in st.session_state:
        st.session_state.saludos = []

    name = st.text_input("¿Cuál es tu nombre?", key="name")

    if st.button("Saludar"):
        if name and name.isalpha():
            saludo = f"Hola, {name}, gusto en conocerte.\n"
            st.session_state.saludos.append(saludo)
            st.write("\n".join(st.session_state.saludos))
        elif name:
            st.write("Error: Ingresa un nombre con letras del alfabeto.")

    if st.button("Limpiar saludos"):
        st.session_state.saludos = []
        st.write("La lista de saludos ha sido limpiada.")

# 2. Suma de dos números
def ejercicio_suma():
    num1 = st.number_input("Ingresa el primer número", step=1.0, key="num1")
    num2 = st.number_input("Ingresa el segundo número", step=1.0, key="num2")
    
    if st.button("Sumar"):  
        result = num1 + num2
        st.write(f"El resultado de la suma es: {result}")

# 3. Área de un triángulo
def ejercicio_area_triangulo():
    altura = st.number_input("Ingresa la altura del triángulo", step=0.1, key="altura")
    base = st.number_input("Ingresa la base del triángulo", step=0.1, key="base")
    
    if st.button("Calcular área"): 
        area = (1 / 2) * base * altura
        st.write(f"El área del triángulo es: {area}")

# 4. Calculadora de descuento
def ejercicio_calculadora_descuento():
    precio_original = st.number_input("Ingresa el precio original del producto", step=0.1, key="precio_original")
    descuento = st.number_input("Ingresa el porcentaje de descuento", step=0.1, value=10.0, key="descuento")
    impuesto = st.number_input("Ingresa el porcentaje de impuesto", step=0.1, value=16.0, key="impuesto")
    
    if st.button("Calcular precio final"): 
        precio_con_descuento = precio_original - (descuento * (precio_original / 100))
        precio_final = precio_con_descuento + (impuesto * (precio_con_descuento / 100))
        st.write(f"El precio final después de aplicar el descuento e impuesto es: {precio_final:.2f} pesos.")

# 5. Suma de una lista de números
def ejercicio_suma_lista():
    numeros = st.text_input("Ingresa una lista de números separados por espacios", key="numeros_lista")
    
    if st.button("Sumar lista"): 
        if numeros:
            lista_numeros = [float(num) for num in numeros.split()]
            resultado = sum(lista_numeros)
            st.write(f"La suma de los números es: {resultado}")

# 6. Valores predeterminados
def ejercicio_valores_predeterminados():
    nombre_producto = st.text_input("Nombre del producto", value="producto", key="nombre_producto")
    cantidad = st.number_input("Cantidad", step=1.0, value=1.0, key="cantidad")
    precio_por_unidad = st.number_input("Precio por unidad", step=0.1, value=10.0, key="precio_por_unidad")

    if st.button("Calcular precio total"): 
        precio_total = cantidad * precio_por_unidad
        st.write(f"El precio total por {cantidad:.0f} {nombre_producto}(s) es: {precio_total:.2f} pesos.")

# 7. Pares e impares
def ejercicio_pares_e_impares():
    numeros = st.text_input("Ingresa los números separados por espacios", key="numeros")
    
    if st.button("Calcular pares e impares"):  
        if numeros:
            lista_numeros = list(map(float, numeros.split()))
            pares = [num for num in lista_numeros if num % 2 == 0]
            impares = [num for num in lista_numeros if num % 2 != 0]
            st.write(f"Números pares: {pares}")
            st.write(f"Números impares: {impares}")

# 8. Multiplicación con *args
def ejercicio_multiplicacion_args():
    numeros = st.text_input("Ingresa los números separados por espacios", key="numeros_multiplicacion")
    
    if st.button("Multiplicar"): 
        if numeros:
            lista_numeros = list(map(float, numeros.split()))
            resultado = 1
            for num in lista_numeros:
                resultado *= num
            st.write(f"El resultado de la multiplicación es: {resultado}")
        else:
            st.write("El resultado de la multiplicación es: 1")

# 9. Información de una persona
def ejercicio_informacion_personal():
    nombre = st.text_input("Ingresa tu nombre", key="nombre_info")
    edad = st.number_input("Ingresa tu edad", min_value=0.0, key="edad_info")
    direccion = st.text_input("Ingresa tu dirección", key="direccion_info")
    
    if st.button("Mostrar información"): 
        st.write(f"Nombre: {nombre}")
        st.write(f"Edad: {edad:.0f}")
        st.write(f"Dirección: {direccion}")

# 10. Calculadora flexible
def ejercicio_calculadora_flexible():
    num1 = st.number_input("Ingresa el primer número", step=0.1, key="num1_calc")
    num2 = st.number_input("Ingresa el segundo número", step=0.1, key="num2_calc")
    operacion = st.selectbox("Selecciona la operación", ["suma", "resta", "multiplicación", "división"], index=0)

    if st.button("Calcular"): 
        if operacion == "suma":
            resultado = num1 + num2
        elif operacion == "resta":
            resultado = num1 - num2
        elif operacion == "multiplicación":
            resultado = num1 * num2
        elif operacion == "división":
            resultado = num1 / num2 if num2 != 0 else "Error: División por cero"
        
        st.write(f"El resultado de la operación es: {resultado}")

with tabs[0]:
    ejercicio_saludo()

with tabs[1]:
    ejercicio_suma()

with tabs[2]:
    ejercicio_area_triangulo()

with tabs[3]:
    ejercicio_calculadora_descuento()

with tabs[4]:
    ejercicio_suma_lista()

with tabs[5]:
    ejercicio_valores_predeterminados()

with tabs[6]:
    ejercicio_pares_e_impares()

with tabs[7]:
    ejercicio_multiplicacion_args()

with tabs[8]:
    ejercicio_informacion_personal()

with tabs[9]:
    ejercicio_calculadora_flexible()

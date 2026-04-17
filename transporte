import streamlit as st
import numpy as np
import pandas as pd

st.title("🏭 Optimización de Demanda por CEDIS")

# -------------------------
# DEMANDA TOTAL
# -------------------------
st.header("📊 Demanda")

demanda_total = st.number_input("Demanda total (pedidos)", value=300)

# -------------------------
# CEDIS
# -------------------------
st.header("🏭 Centros de Distribución")

num_cedis = st.number_input("Número de CEDIS", min_value=1, value=2)

cedis = []
capacidades = []

for i in range(int(num_cedis)):
    nombre = st.text_input(f"Nombre CEDIS {i+1}", value=f"CEDIS {i+1}")
    cap = st.number_input(f"Capacidad total {nombre}", value=150)
    
    cedis.append(nombre)
    capacidades.append(cap)

# -------------------------
# OPTIMIZACIÓN
# -------------------------
st.header("⚙️ Asignación Óptima")

restante = demanda_total
data = []

for i in range(len(cedis)):
    asignado = min(restante, capacidades[i])
    restante -= asignado
    
    data.append([cedis[i], asignado])

if restante > 0:
    data.append(["Demanda no cubierta", restante])

df = pd.DataFrame(data, columns=["CEDIS", "Pedidos asignados"])

# -------------------------
# VIAJES
# -------------------------
st.header("🚛 Cálculo de viajes")

capacidad_vehiculo = st.number_input("Capacidad por vehículo (pedidos)", value=20)

df["Viajes"] = np.ceil(df["Pedidos asignados"] / capacidad_vehiculo)

# -------------------------
# RESULTADOS
# -------------------------
st.subheader("📋 Distribución de demanda")

st.dataframe(df)

total_viajes = df["Viajes"].sum()
st.write(f"Total de viajes: {total_viajes}")

# -------------------------
# ANÁLISIS
# -------------------------
st.header("📈 Análisis")

if restante > 0:
    st.error("⚠️ No se puede cubrir toda la demanda con la capacidad actual")
else:
    st.success("✅ Demanda cubierta correctamente")

import numpy as np
import matplotlib.pyplot as plt

# =========================================================
# 1. PARÁMETROS TEÓRICOS DEL EXPERIMENTO
# =========================================================
mu_0 = 4 * np.pi * 1e-7  # Permeabilidad magnética del vacío [H/m]
D = 0.1256               # Diámetro de la bobina en metros (aprox 12.56 cm, deducido del tablero)

# =========================================================
# 2. GRÁFICA 1: B vs I (N como parámetro)
# =========================================================
plt.figure(figsize=(8, 5))
I_array = np.linspace(0, 0.5, 100)  # Corriente de 0 a 500 mA (0.5 A)
N_valores = [5, 10, 15]             # Espiras evaluadas en la guía

for N in N_valores:
    # B = (mu_0 * N * I / D), se multiplica por 1e6 para pasar a microTeslas (uT)
    B_I = (mu_0 * N * I_array / D) * 1e6 
    plt.plot(I_array, B_I, label=f'N = {N} espiras', linewidth=2)

plt.title('Comportamiento Teórico: Campo Magnético vs Corriente', fontsize=12, fontweight='bold')
plt.xlabel('Corriente Eléctrica, I [A]', fontsize=11)
plt.ylabel('Campo Magnético en el centro, B [µT]', fontsize=11)
plt.legend(loc='upper left')
plt.grid(True, linestyle='--', alpha=0.7)
plt.xlim(0, 0.55)
plt.ylim(0, 80)
plt.tight_layout()
plt.savefig('grafica_B_vs_I.png', dpi=300)
plt.show()

# =========================================================
# 3. GRÁFICA 2: B vs N (I como parámetro)
# =========================================================
plt.figure(figsize=(8, 5))
N_array = np.linspace(0, 15, 100)   # Rango continuo de espiras para la línea teórica
I_valores = [0.1, 0.3, 0.5]         # Muestras de corriente: 100mA, 300mA, 500mA

for I in I_valores:
    B_N = (mu_0 * N_array * I / D) * 1e6
    plt.plot(N_array, B_N, label=f'I = {int(I*1000)} mA', linewidth=2)

plt.title('Comportamiento Teórico: Campo Magnético vs Número de Espiras', fontsize=12, fontweight='bold')
plt.xlabel('Número de Espiras, N', fontsize=11)
plt.ylabel('Campo Magnético en el centro, B [µT]', fontsize=11)
plt.legend(loc='upper left')
plt.grid(True, linestyle='--', alpha=0.7)
plt.xlim(0, 16)
plt.ylim(0, 80)
plt.tight_layout()
plt.savefig('grafica_B_vs_N.png', dpi=300)
plt.show()

# =========================================================
# 4. GRÁFICA 3: B vs NI (Modelo para Regresión Lineal)
# =========================================================
plt.figure(figsize=(8, 5))
# El valor máximo de NI es N_max * I_max = 15 * 0.5 A = 7.5 A
NI_array = np.linspace(0, 7.5, 100) 
B_NI = (mu_0 * NI_array / D) * 1e6

plt.plot(NI_array, B_NI, color='purple', label=r'Teórico: $B = \frac{\mu_0}{D}(NI)$', linewidth=2.5)

plt.title('Comportamiento Teórico: Campo Magnético vs Variable NI', fontsize=12, fontweight='bold')
plt.xlabel('Producto (Número de espiras × Corriente), NI [A]', fontsize=11)
plt.ylabel('Campo Magnético en el centro, B [µT]', fontsize=11)
plt.legend(loc='upper left', fontsize=11)
plt.grid(True, linestyle='--', alpha=0.7)
plt.xlim(0, 8)
plt.ylim(0, 80)
plt.tight_layout()
plt.savefig('grafica_B_vs_NI.png', dpi=300)
plt.show()

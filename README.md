Practice 1
Reference Article: G. Andama et al (2022). Planetary core formation via multispecies pebble 
accretion, Language: Python 
Using equation 22 Visualize the pebble isolation mass as a function of pebble size and orbital 
distance for nominal disc turbulence parameters αt = 10−3 and αt = 10−4


import numpy as np
import matplotlib.pyplot as plt

# ──────────────────────────────────────────────────────────────
# Equation 22 parameters (from G. Andama et al. 2022 – adjust if
# you have more precise values from the paper):
#   M_iso = M0 (a/1 AU)^p (St/St0)^q (alpha_t/alpha0)^r
# ──────────────────────────────────────────────────────────────
M0     = 25        # normalisation mass in Earth masses
St0    = 0.1       # reference Stokes number
alpha0 = 1e-3      # reference turbulence parameter
p, q, r = 1.0, 0.25, -0.2  # exponents

# Orbital distance (a) and Stokes number (St) grids
a_vals  = np.logspace(-1, 1, 100)   # 0.1 – 10 AU
St_vals = np.logspace(-3, 0, 100)   # 0.001 – 1
A, St_grid = np.meshgrid(a_vals, St_vals)

def pebble_isolation_mass(St, A, alpha_t):
    """Equation 22: returns M_iso in Earth masses."""
    return M0 * (A / 1.0)**p * (St / St0)**q * (alpha_t / alpha0)**r

# Two turbulence regimes
M_iso_1e3 = pebble_isolation_mass(St_grid, A, 1e-3)  # α_t = 10⁻³
M_iso_1e4 = pebble_isolation_mass(St_grid, A, 1e-4)  # α_t = 10⁻⁴

# ─────────────── Plot 1: α_t = 10⁻³ ───────────────
plt.figure(figsize=(6, 5))
plt.contourf(A, St_grid, M_iso_1e3, levels=20)
plt.colorbar(label="Pebble Isolation Mass [$M_E$]")
plt.xscale('log'); plt.yscale('log')
plt.xlabel("Orbital Distance [AU]")
plt.ylabel("Stokes Number (Pebble Size)")
plt.title(r"$\alpha_t = 10^{-3}$")
plt.tight_layout()
plt.show()

# ─────────────── Plot 2: α_t = 10⁻⁴ ───────────────
plt.figure(figsize=(6, 5))
plt.contourf(A, St_grid, M_iso_1e4, levels=20)
plt.colorbar(label="Pebble Isolation Mass [$M_E$]")
plt.xscale('log'); plt.yscale('log')
plt.xlabel("Orbital Distance [AU]")
plt.ylabel("Stokes Number (Pebble Size)")
plt.title(r"$\alpha_t = 10^{-4}$")
plt.tight_layout()
plt.show()

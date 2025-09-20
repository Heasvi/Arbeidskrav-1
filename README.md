# Arbeidskrav-1
Calculating the difference in car cost

"""
Anta at du skal kjøpe bil. Det står mellom elbil og bensinbil, og du ønsker å sammenlikne de årlige kostnadene ved elbil sammenliknet med bensinbil.

Lag et Python-program som beregner og presenterer (i konsollen) de årlige totalkostnadene for elbil og for bensinbil samt årlig kostnadsdifferanse basert på informasjonen gitt nedenfor. Du kan her for enkelhets skyld se bort fra kostnader som renter på billån og verditap (du har da egentlig antatt at slike kostnader er like for elbil og bensinbil).

Nedenfor er informasjon som programmet skal baseres på (som selvsagt kan diskuteres, men ikke ifm. denne oppgaven :-)

Du kan selv velge antall kjørte km/år ut fra din typiske bilbruk. Ev. (hvis du ikke har bil) kan du anta 10.000 km.
Forsikring: Elbil: 5000 kr/år. Bensinbil: 7500 kr/år.
Trafikkforsikringsavgift: 8,38 kr/dag for både elbil og bensinbil.
Drivstoffbruk: Elbil: 0,2 kWh/km. Strømpris (antar kun hjemmelading): 2.00 kr/kWh. Bensinbil: 1,0 kr/km.
Bomavgift: Elbil: 0,1 kr/km. Bensinbil: 0,3 kr/km.
"""

import pandas as pd
import matplotlib.pyplot as plt
import numpy as np


#Forsikring

forsikring_el = 5000 # [kr/år]
forsikring_bensin = 7500 # [kr/år]

trafikkavg = 8.38 # [kr/dag]

#Forbruk

drivstoff_fbr_el = 0.2 # [kWh/km]
drivstoff_fbr_bensin = 1.0 # [kr/km]

#Pris

strøm_pris = 2.0 # [kr/kWh]

#Bomavgift

bom_el = 0.1 # [kr/km]
bom_bensin = 0.3 # [kr/km]

#Kjørte km/år

kjørte_km = 50000


#Kostnad

årlig_kost_el = forsikring_el + (trafikkavg*365) + (drivstoff_fbr_el * kjørte_km)*strøm_pris + (bom_el * kjørte_km)

årlig_kost_bensin = forsikring_bensin + (trafikkavg*365) + (drivstoff_fbr_bensin * kjørte_km) + (bom_bensin * kjørte_km)

diff_kost = abs(årlig_kost_el - årlig_kost_bensin)



#Utregning over flere år
total_el_liste = []
total_bensin_liste = []
diff_kost_liste= []

for antall_år in range(1,11):
    totalt_el = antall_år * årlig_kost_el
    totalt_bensin = antall_år * årlig_kost_bensin
    akkumulert_diff_kost = antall_år * diff_kost
    total_el_liste.append(totalt_el)
    total_bensin_liste.append(totalt_bensin)
    diff_kost_liste.append(akkumulert_diff_kost)
    
    

plt.plot(range(1,11),total_el_liste, label="Elbil")
plt.plot(range(1,11),total_bensin_liste, label = "Bensinbil")
plt.plot(range(1,11), diff_kost_liste, label = "Differanse")
plt.legend()
plt.grid(True)
plt.ylabel("Kostnader")
plt.xlabel("Antall år")
plt.show()

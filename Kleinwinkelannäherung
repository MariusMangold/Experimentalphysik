import math

import numpy as np
from numpy import sin, cos
from scipy.integrate import odeint
from matplotlib import pyplot as plt


# Definition der Gleichung
def gleichungen(y0, t):
    phi, x = y0
    f = [x, -(g / l) * sin(phi)]
    return f


# definition des Schaubildes

def schaubild(zeit, phi1, phi2):
    plt.plot(zeit, phi1[:, 0])
    plt.plot(zeit, phi2)
    s = '(Anfangswinkel = ' + str(winkel_start) + ' grad)'
    plt.title('Das Fadenpendel: ' + s)
    plt.xlabel('zeit (s)')
    plt.ylabel('winkel (rad)')
    plt.grid(True)
    plt.legend(['tatsächlich(1)', 'angenähert(2)'], loc='best')
    plt.text(0, -1.2, r'$\mathcal{T}$ 1:   ' + str(round((t1), 5)) + 's', fontsize=12)
    plt.text(20, -1.2, r'$\mathcal{T}$ 2:   ' + str(round((t2), 5)) + 's', fontsize=12)
    plt.text(40, -1.2, r'$\Delta\mathcal{T}$   ' + str(round((t1 - t2), 5)), fontsize=12)
    plt.text(60, -1.2, 'Zeitspanne:  ' + str(zeitmax) + 's', fontsize=12)
    plt.text(80, -1.2, 'Genauigkeit:  ' + str(zeitschritt) + 's', fontsize=12)
    plt.show()


# parameter
g = 9.81
l = 1.0

zeitmax = 1000
zeitschritt = 0.000001
zeit = np.arange(0, zeitmax, zeitschritt)  # anfangswert, endwert, zeitstücke

# anfangsbedingungen
winkel_start = (1 / 4)  # eingabe des startwinkels in pi
phi0 = winkel_start * math.pi  # konvertgesuchtezeit= zeitmax-(zaehler*zeitschritt)ierung in rad
v0 = np.radians(0)  # Eingabe der Startgeschwindigkeit

# find the solution to the nonlinear problem
phi1 = odeint(gleichungen, [phi0, v0], zeit)

# find the solution to the linear problem
w = np.sqrt(g / l)
phi2 = [phi0 * cos(w * t) for t in zeit]

a = np.array(phi1)
b = (a[:, 0])
print(b)

# Maximalbestimmung phi1
numbermid1 = 1
numberold1 = 1
latest1 = 0
counter1 = -1
zaehler1 = 0
# maximazählung , counter= anzahl der Maxima        latest= wert des letzten maximums
for number1 in b:
    if numbermid1 >= number1 and numbermid1 >= numberold1:
        counter1 += 1
        latest1 = number1
    numberold1 = numbermid1
    numbermid1 = number1

# suche des letzten maximums     zeitschritte zum finden = zaehler
for suche1 in b[::-1]:
    if latest1 == suche1:
        break
    else:
        zaehler1 += 1

# Umlaufzeit T1 = anzahl der maxima / (ganze zeit- zeitspanne zum letzten maximum)
# t1 = counter / (zeitmax-(zaehler*zeitschritt)
gesuchtezeit1 = zeitmax - (zaehler1 * zeitschritt)
print('numerische umläufe   ' + str(counter1))
print('numerische zeit bis letztes maximum    ' + str(gesuchtezeit1))

# t1 = Umlaufzeit der kleinwinkelannäherung
t1 = gesuchtezeit1 / counter1
print('Tnumerisch1     ' + str(t1))



# Maximabstimmung phi2
numbermid2 = 1
numberold2 = 1
latest2 = 0
counter2 = -1
zaehler2 = 0
# maximazählung , counter= anzahl der Maxima        latest= wert des letzten maximums
for number2 in phi2:
    if numbermid2 >= number2 and numbermid2 >= numberold2:
        counter2 += 1
        latest2 = number2
    numberold2 = numbermid2
    numbermid2 = number2

# suche des letzten maximums     zeitschritte zum finden = zaehler
for suche2 in phi2[::-1]:
    if latest2 == suche2:
        break
    else:
        zaehler2 += 1

# Umlaufzeit T2 = anzahl der maxima / (ganze zeit- zeitspanne zum letzten maximum)
# t2 = counter / (zeitmax-(zaehler*zeitschritt)
gesuchtezeit2 = zeitmax - (zaehler2 * zeitschritt)
print('2genäherte umläufe   ' + str(counter2))
print('2genäherte zeit bis letztes maximum    ' + str(gesuchtezeit2))

# t2 = Umlaufzeit der kleinwinkelannäherung
t2 = gesuchtezeit2 / counter2
print('T2     ' + str(t2))

deltaT = t1 - t2
print('deltaT : ' + str(deltaT))
# plot the results
#schaubild(zeit, phi1, phi2)

# deltaT = numerisch- genähert

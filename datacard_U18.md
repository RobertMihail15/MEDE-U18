# Data Card – U18
## Wearable multimodal pentru analiza efortului fizic

**Cod unitate:** U18  
**Întrebare:** Ce adaugă pulsul/conductanța la accelerometru (efort/stres)?  
**Focus ales:** efort fizic  
**Unitatea de analiză:** persoană × fereastră temporală de 2–10 s

Proiectul utilizează două surse multimodale de date provenite de la
dispozitive wearable: PAMAP2 și MHEALTH. Ambele conțin informații
despre mișcare și informații fiziologice, permițând compararea unei
reprezentări bazate doar pe accelerometru cu una care include și
informație cardiacă.


# Sursa 1 – PAMAP2 Physical Activity Monitoring Dataset

## 1. Proveniență

**Repository:** UCI Machine Learning Repository  
**Dataset:** PAMAP2 Physical Activity Monitoring  
**Creator:** Attila Reiss  
**Publicat/donat UCI:** 5 august 2012  
**DOI:** 10.24432/C5NW2H  
**Licență:** Creative Commons Attribution 4.0 International (CC BY 4.0)

**Referință asociată:**  
Reiss, A. & Stricker, D. (2012),  
*Introducing a New Benchmarked Dataset for Activity Monitoring.*

**Perioada exactă de colectare:** nespecificată în documentația consultată.


## 2. Participanți și activități

Datasetul conține date provenite de la **9 participanți**.

Sunt disponibile **18 tipuri de activități** în total:
12 activități aparțin protocolului principal, iar 6 sunt activități
opționale.

Activitățile includ, printre altele:
- lying
- sitting
- standing
- walking
- running
- cycling
- Nordic walking
- ascending stairs
- descending stairs
- vacuum cleaning
- ironing
- rope jumping

**Activity ID 0** reprezintă categoria „other”, utilizată pentru
activități tranzitorii. Aceasta nu va fi considerată o activitate
propriu-zisă în analiza ulterioară.


## 3. Senzori și modalități

Participanții poartă trei unități inerțiale (IMU), amplasate la:

- mâna dominantă
- piept
- gleznă

În plus, este utilizat un monitor de ritm cardiac.

Fiecare IMU furnizează:

- temperatură
- accelerometru 3D ±16g
- accelerometru 3D ±6g
- giroscop 3D
- magnetometru 3D
- orientare

Datele de orientare sunt marcate în documentație ca invalide pentru
această colectare și nu vor fi utilizate în analiză.


## 4. Rezoluție temporală

**IMU:** 100 Hz  
**Heart rate:** aproximativ 9 Hz

Diferența dintre frecvențele de eșantionare va necesita alinierea
informației de mișcare cu informația cardiacă la nivelul ferestrelor
temporale utilizate în analiză.


## 5. Structura datelor

Fiecare înregistrare PAMAP2 conține **54 de coloane**:

- coloana 1: timestamp
- coloana 2: activity ID
- coloana 3: heart rate
- coloanele 4–20: IMU hand
- coloanele 21–37: IMU chest
- coloanele 38–54: IMU ankle

Fiecare grup IMU conține 17 variabile corespunzătoare temperaturii,
accelerometrelor, giroscopului, magnetometrului și orientării.


## 6. Unități de măsură

| Variabilă | Unitate |
|---|---|
| Timestamp | s |
| Heart rate | bpm |
| Temperatură | °C |
| Accelerație | m/s² |
| Giroscop | rad/s |
| Magnetometru | µT |


## 7. Goluri și calitatea datelor

Documentația UCI indică existența valorilor lipsă.

Valorile lipsă sunt reprezentate prin `NaN`.

O cauză importantă pentru numărul ridicat de valori lipsă din coloana
heart rate este diferența dintre frecvența IMU (100 Hz) și frecvența
monitorului cardiac (~9 Hz).

**Verificare preliminară realizată în notebook:**

- fișier: `subject101.dat`
- dimensiune: 376.417 rânduri × 54 coloane
- valori lipsă heart rate: aproximativ 90,86%

Acest procent se referă la fișierul verificat și nu este generalizat
automat la întregul dataset.


## 8. Rol în proiect

PAMAP2 va fi utilizat pentru investigarea diferenței dintre:

**accelerometru**

și

**accelerometru + ritm cardiac**

în caracterizarea efortului fizic.

Datasetul permite observarea simultană a mișcării corpului și a
răspunsului cardiac asociat activității.


# Sursa 2 – MHEALTH Dataset

## 1. Proveniență

**Repository:** UCI Machine Learning Repository  
**Dataset:** MHEALTH (Mobile Health)  
**Creators:** Oresti Banos, Rafael Garcia, Alejandro Saez  
**Publicat/donat UCI:** 6 decembrie 2014  
**DOI:** 10.24432/C5TW22  
**Licență:** Creative Commons Attribution 4.0 International (CC BY 4.0)

**Referință asociată:**  
Banos, O. et al. (2014),  
*mHealthDroid: A Novel Framework for Agile Development of Mobile
Health Applications.*

**Perioada exactă de colectare:** nespecificată în documentația consultată.


## 2. Participanți și activități

Datasetul conține date provenite de la **10 participanți**.

Participanții realizează **12 activități fizice**, printre care:

- standing
- sitting and relaxing
- lying down
- walking
- climbing stairs
- waist bends forward
- frontal elevation of arms
- knees bending
- cycling
- jogging
- running
- jumping front and back

**Label 0** reprezintă clasa null, adică perioade care nu aparțin
celor 12 activități definite.


## 3. Senzori și modalități

Senzorii sunt amplasați în trei zone ale corpului:

- piept
- gleznă stângă
- braț drept

Datele disponibile includ:

- accelerometru
- giroscop
- magnetometru
- ECG cu două canale

Senzorul de la piept furnizează accelerație și două canale ECG.
Senzorii de la gleznă și braț furnizează informații inerțiale.


## 4. Rezoluție temporală

Datele sunt înregistrate la o frecvență de:

**50 Hz**

Modalitățile sunt furnizate împreună în fișierele individuale ale
participanților.


## 5. Structura datelor

Datele fiecărui participant sunt stocate într-un fișier `.log`
separat.

Fiecare fișier conține **24 de coloane**.

### Piept
- 3 axe accelerometru
- ECG lead 1
- ECG lead 2

### Gleznă stângă
- 3 axe accelerometru
- 3 axe giroscop
- 3 axe magnetometru

### Braț drept
- 3 axe accelerometru
- 3 axe giroscop
- 3 axe magnetometru

### Etichetă
- activity label

Valoarea `0` este utilizată pentru clasa null.


## 6. Unități de măsură

| Variabilă | Unitate |
|---|---|
| Accelerație | m/s² |
| Giroscop | deg/s |
| ECG | mV |
| Câmp magnetic | „local”, conform documentației UCI |

Documentația consultată nu furnizează o unitate fizică mai precisă
pentru câmpul magnetic, astfel că este păstrată formularea oficială
„local”.


## 7. Goluri și calitatea datelor

Pagina UCI indică:

**Has Missing Values? No**

Prin urmare, conform documentației oficiale, datasetul nu conține
valori lipsă.

**Verificare preliminară realizată în notebook:**

- fișier: `subject1.log`
- dimensiune: 161.280 rânduri × 24 coloane
- valori NaN identificate: 0

Verificarea proprie confirmă situația pentru fișierul analizat.


## 8. Rol în proiect

MHEALTH va fi utilizat ca sursă complementară pentru investigarea
relației dintre informația de mișcare și informația cardiacă.

Spre deosebire de PAMAP2, MHEALTH nu furnizează direct heart rate,
ci două canale ECG.

Pentru realizarea unei comparații la nivelul informației cardiace,
din ECG va fi derivată ulterior o reprezentare adecvată, precum
ritmul cardiac.


# Relația dintre cele două surse

Cele două dataseturi oferă două configurații multimodale:

**PAMAP2:** accelerometru + heart rate  
**MHEALTH:** accelerometru + ECG

Participanții din cele două dataseturi sunt diferiți. Prin urmare,
sursele nu vor fi concatenate sau aliniate între ele la nivel de
participant sau rând.

Fiecare dataset va fi analizat separat.

În interiorul fiecărei surse, analiza va compara informația obținută
din mișcare cu informația obținută prin adăugarea componentei
cardiace.

Comparația principală urmărită este:

**accelerometru**
vs.
**accelerometru + informație cardiacă**

Rezultatele obținute pe cele două surse vor putea fi ulterior
comparate pentru a verifica dacă tendințele observate sunt
consistente între dataseturi.


# Limitări și aspecte de urmărit

1. PAMAP2 înregistrează IMU și heart rate la frecvențe diferite
   (100 Hz vs. aproximativ 9 Hz), fiind necesară o strategie de
   aliniere temporală.

2. PAMAP2 furnizează direct heart rate, în timp ce MHEALTH
   furnizează ECG. Reprezentarea informației cardiace trebuie
   definită astfel încât comparația să rămână coerentă.

3. Participanții diferă între cele două surse, astfel încât
   dataseturile vor fi analizate separat.

4. Unitățile giroscopului diferă:
   PAMAP2 utilizează rad/s, iar MHEALTH deg/s.

5. Datele de orientare din PAMAP2 sunt marcate ca invalide și nu
   vor fi utilizate.


# Surse de documentare

1. UCI Machine Learning Repository –
   PAMAP2 Physical Activity Monitoring Dataset.
   DOI: 10.24432/C5NW2H

2. Reiss, A., Stricker, D. (2012).
   Introducing a New Benchmarked Dataset for Activity Monitoring.

3. UCI Machine Learning Repository –
   MHEALTH Dataset.
   DOI: 10.24432/C5TW22

4. Banos, O., Garcia, R., Holgado-Terriza, J. A., Damas, M.,
   Pomares, H., Rojas, I., Saez, A., Villalonga, C. (2014).
   mHealthDroid: A Novel Framework for Agile Development of
   Mobile Health Applications.

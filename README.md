# Documentatie Proiect Three.js — Sistem Solar Interactiv

## Autor
[Dahrouj_Joudi_grupa1116]

## Descriere generala
Aplicatia reprezinta o simulare interactiva a Sistemului Solar,
construita cu Three.js r101. Utilizatorul poate naviga liber prin
scena 3D, interactiona cu planetele prin mouse si tastatura, si
controla parametrii animatiei prin interfata dat.GUI.

---

## Structura fisierelor

```
Dahrouj_Joudi_grupa1116/
├── index.html          ← aplicatia principala (tot codul)
├── three.js            ← libraria Three.js r101
├── three.min.js        ← versiunea minificata Three.js
├── three.module.js     ← versiunea ES module Three.js
├── OrbitControls.js    ← addon pentru controlul camerei cu mouse
├── dat.gui.js          ← libraria pentru interfata GUI
├── jquery-3.3.1.js     ← jQuery (inclus in arhiva)
└── README.md           ← acest document
```

---

## Elemente tehnice implementate (Baremul de 4p)

### 1. Scena de baza (3p)
- Scena Three.js cu WebGLRenderer, PerspectiveCamera
- Soare central cu geometrie SphereGeometry (raza 12)
- 8 planete (Mercur, Venus, Terra, Marte, Jupiter, Saturn, Uranus, Neptun)
- Orbite vizibile desenate cu LineLoop si BufferGeometry
- Inele pentru Saturn (RingGeometry cu UV-uri ajustate)

### 2. Materiale, Texturi Complexe si Lumini (1p)
Texturi procedurale generate cu Canvas API:
- **Soare**: gradient radial galben-portocaliu + pete solare
- **Terra**: oceane albastre + continente verzi + nori semitransparenti
- **Marte**: suprafata roscata cu crateri
- **Jupiter**: benzi atmosferice colorate + Pata Rosie Mare
- **Saturn**: benzi de culori calde
- Celelalte planete: gradiente radiale unice

Lumini utilizate:
- `PointLight` (Soare) — lumina principala cu umbre
- `AmbientLight` — iluminare ambientala slaba
- `HemisphereLight` — atmosfera generala

Materiale:
- `MeshStandardMaterial` pentru planete (roughness, metalness)
- `MeshBasicMaterial` pentru Soare si halo
- `PointsMaterial` pentru particule (stele, asteroizi)

### 3. Geometrii Proprii Complexe (1p)
**Asteroid Belt** (centura intre Marte si Jupiter):
- `BufferGeometry` creat manual cu `setAttribute`
- 4000 particule pozitionate procedural in inel
- Raza interioara 78, exterioara 98 unitati
- Coordonate calculate cu functii trigonometrice
- Culori per-vertex (gri-maronii variabile)

### 4. Particule (1p)
**Camp de stele** (12,000 particule):
- `BufferGeometry` cu pozitii distribuite sferic
- Raza 600-1400 unitati
- 4 tipuri de stele: albe, albastrui, galbene, rosiatice
- Marimea variabila per-particula
- Distributie uniforma pe sfera (algoritm phi/theta)

### 5. Manipulare cu Mouse si Tastatura (1p)
**Mouse:**
- Drag stanga = rotire camera (OrbitControls)
- Scroll = zoom in/out
- Click pe planeta = focus automat + afisare nume

**Tastatura:**
- `1`-`8` = focusare rapida pe planeta
- `R` = reset camera la pozitia initiala
- `P` = toggle pauza animatie
- `+`/`-` = crestere/scadere viteza globala

### 6. Controale dat.GUI (1p)
Panoul GUI (dreapta sus) ofera:
- **Viteza animatie** (slider 0-5)
- **Pauza** (checkbox)
- **Intensitate Soare** (slider 0-5, modifica PointLight)
- **Reset Camera** (buton)
- **Viteze Individuale** (folder cu slider per planeta)

---

## Complexitate si Coerenta (2p)
- Tema coerenta: sistem solar cu fizica simplificata
- Pivoti de orbita separati per planeta (Object3D nested hierarchy)
- Unghi initial diferit per planeta (distributie uniforma)
- Lerp camera pentru tranzitii fluide la focus
- Umbre activate (castShadow / receiveShadow)
- Halo semi-transparent in jurul Soarelui
- Label animat la selectarea unei planete
- Responsive (resize listener)



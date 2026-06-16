# CSARCH2 Virtual Exhibit Case Proposal

**Term:** 3rd Term 2025-2026  
**Section:** S40 (Category: How it Works)  
**Group Title:** Kahit Ano

## Group Member Roster

1. Hannah Tayzon - [Role]
2. Hans Gabriel Obcena - [Role]
3. James Edsel Alvarez - [Role]
4. Jarick Viray - [Role]
5. Lorenzo Suerte - [Role]

---

# Group Topic Theme

## The Digitizer Matrix & Pressure-Sensitive Technology
### (How Drawing Tablets Work)

### What is the theme's focus?

1. The exhibit’s main goal is to explain the technicalities of how drawing tablets interpret and communicate a user’s analog input. The exhibit will demonstrate how two technologies work together in order to achieve what a drawing tablet can provide.

2. The two technologies that will be tackled in this exhibit are:
   - **Digitizer Matrix** (X, Y spatial tracking)
   - **Pressure-Sensitive Technology** (Z-axis force quantization)

### What will the theme explicitly discuss?

## 1. The Coordinate Plane: The Digitizer Matrix (X, Y Spatial Tracking)

### Hardware and Architecture

- The drawing tablet’s surface consists of grids of tiny wires.
- These grids contain conductive traces that detect the current position of the pen through electromagnetic or capacitive sensing techniques.

## 2. The Force Plane: Pressure-Sensitive Technology (Z-Axis Force Quantization)

### Hardware and Architecture

- The tip of the pen has a pressure-sensitive mechanism.
- When the pen is pressed down onto the tablet, the sensor is physically squeezed.
- That physical squeeze is translated into a digital measurement that tells the computer how hard the user is pressing onto the tablet.

## 3. The Reporting Process

### How the Tablet Communicates Data to the CPU

#### Hardware and Architecture

- Once the drawing tablet has gathered the data from these two components, it is sent as a single data packet.
- This packet triggers a hardware interrupt.
- The interrupt tells the CPU to process the analog input and convert it into a visible stroke or line on the screen.

---

# Group Tech Stack Plan

## Core Stack & Dependencies

- **Runtime System:** Node.js 26
- **Web Framework:** Astro 6
- **Content Format:** MDX (Markdown Extended) for embedding components inside the exhibit article
- **Interactive Engine:** React (`.jsx`) for client-side state, simulations, and animations
- **Low-Level Logic Simulations:** C/C++

---

# Repository Map

```text
/
├── astro.config.mjs
├── package.json
├── package-lock.json
├── tsconfig.json
└── src/
    ├── components/
    │   ├── InteractiveCanvas.jsx
    │   ├── HardwareMatrixSim.jsx
    │   └── BusRegisterMonitor.jsx
    ├── layouts/
    │   └── ExhibitLayout.astro
    └── pages/
        └── drawing-tablet.mdx
```

---

# Proposed Interactive Element

## 1. Hovering/Dragging Cursor over the Simulated Pad Area

### User Interaction
The user moves the cursor across the virtual drawing tablet surface.

### Visual React Animation
- The cursor acts as a digital pen.
- Copper wire paths beneath the pen tip illuminate as it moves.
- The user can visually observe the active sensing area.

### Hardware Architecture Logic
- The Digitizer Matrix samples the pen position.
- X and Y coordinate values are stored in memory-mapped registers.
- The system continuously tracks the pen's location.

---

## 2. Adjusting the Force Slider

### User Interaction
The user adjusts a slider representing the pressure applied to the pen.

### Visual React Animation
- A force monitor displays the current pressure level.
- The displayed value changes in real time as the slider moves.

### Hardware Architecture Logic
- A simulated ADC samples pressure sensor readings.
- Analog pressure values are converted into digital values.
- Values are scaled into an 8,192-level pressure range (13-bit resolution).
- Demonstrates analog-to-digital quantization.

---

## 3. Sketching Continuously at High Speed

### User Interaction
The user rapidly draws across the tablet surface.

### Visual React Animation
- The monitor displays strokes in real time.
- Stroke thickness changes according to pressure and movement speed.

### Hardware Architecture Logic
- A hardware interrupt is generated.
- The interrupt signals the CPU to process new input.
- The CPU updates the display based on the received data.

---

# Tentative Style Guide Snapshot & Exhibit Layout

## Style Matrix

- **Background Base:** Pure Web White (`#FFFFFF`)
- **Primary Matrix Accent:** Deep Jet Black (`#000000`)
- **Pressure Signal Accent:** Precision Slate Gray (`#555555`)
- **Text Base:** Stark Charcoal Black (`#1A1A1A`)
- **Typography Sets:**
  - Arial (System Sans-Serif)
  - Courier New (System Monospace)

---

# Proposed Page Wireframe Layout

```text
+-----------------------------------------------------------------------------+
|               INTERACTIVE COMPONENT: DRAWING TABLET SIMULATOR              |
+-----------------------------------------+-----------------------------------+
| [ Visual Hardware Simulation ]          | [ Live Architecture Data Feed ]   |
|                                         |                                   |
| +---------------+                       | >> POLLING I/O DEVICE...          |
| | Monitor       |                       | >> INTERRUPT REQUEST: ACTIVE      |
| | (0_0)         |                       |                                   |
| +-------+-------+                       | [ X,Y MATRIX SENSOR DATA ]        |
|         |                               | X-Coordinate: 0x1F4A (8010)       |
| +-------+-------+                       | Y-Coordinate: 0x0C22 (3106)       |
| | CPU / Host    |                       |                                   |
| +-------+-------+                       | [ Z-AXIS PRESSURE SENSOR ]        |
|         |                               | Raw Analog Force: 65%             |
| +-----------+-----------+               | ADC Quantization: 1010011010110   |
| | Drawing Tablet        | /             | Discrete Level: 5334 / 8192       |
| | [Active Area Grid]    | / <- Pen      |                                   |
| +-----------------------+               | [ DATA BUS STREAM ]               |
|                                         | 01001000 01001001 01000100        |
| Pen Force Slider                        | Sending to CPU Buffer...          |
| [======--------------] 65%              |                                   |
+-----------------------------------------+-----------------------------------+
```

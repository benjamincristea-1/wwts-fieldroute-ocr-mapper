# wwts-fieldroute-ocr-mapper
🗺️ Geospatial dispatch mapper, OCR screenshot parser &amp; FedEx parts route optimizer designed for WWTS Field Service Technicians. Architected from handwritten wireframes; code built with Machine Learning AI (Google Gemini).

# 🗺️ WWTS FieldRoute OCR: Automated Work Order Mapper, FedEx Hub Tracker & Mileage Engine

An interactive geospatial dispatch and route-planning web application designed for **Field Service Engineers and Dynamic Server Support Technicians at Worldwide TechServices (WWTS)**

**WWTS FieldRoute OCR** transforms daily hardware repair dispatches by extracting structured work order data directly from mobile screenshots, color-coordinating FedEx part pickups (**Hillside** vs. **Downtown Chicago**), automatically detecting multiple work orders inside the **same building on different floors**, and calculating real-time **Estimated Drive Times**, road mileage, and **$0.40/mile reimbursement payouts**.
> 🤖 **AI Engineering Attribution:** Product requirements, field-service workflow architecture, and handwritten UI/UX wireframes were designed by the author; application code was built and iteratively engineered using **Machine Learning AI (Google Gemini)**.

---

## 🎯 Project Purpose & Real-World Field Problem

Field Server Support Technicians managing high-volume enterprise hardware dispatches (Dell, Lenovo, HP servers, desktops, and laptops) must coordinate multiple moving parts under strict Service Level Agreements (SLAs):
1. **Fragmented Dispatch Portals:** Copying addresses, `WA#` work order numbers, site codes, and contact info from mobile dispatch screenshots into standard map apps one by one wastes valuable morning prep time.
2. **Multi-Floor Downtown High-Rises:** In dense areas like Downtown Chicago, a technician may have **2 or more work orders inside the exact same building on different floors** (e.g., Willis Tower 44th Floor and 71st Floor). Standard maps stack pins on top of each other, hiding the second ticket.
3. **FedEx Parts Turnaround:** Technicians must pick up replacement motherboards, RAID controllers, and fiber transceivers from specific FedEx Ship Centers (**Hillside** `300 Craig Pl` or **Downtown** `1242 S Canal St`) and match the **last 4 digits of the FedEx package number** to the corresponding work order.
4. **Mileage Reimbursement & 45-Mile Rule:** Technicians are reimbursed at **$0.40/mile** from drop locations to consecutive work orders, and qualify for home-base mileage reimbursement when the first or last work order exceeds **45 miles from Home Base**.

**WWTS FieldRoute OCR** solves all four problems in a persistent, zero-backend browser interface.

---

## ✏️ From Handwritten Wireframes to Production App

This project was engineered from the ground up starting with paper product specifications and low-fidelity UI wireframes before directing **Machine Learning AI Gemini** to build the production code:

* **Stage 1 — Functional Spec (`Interactive Map Purpose & List`):** Defined persistent map pins, color-coded stop categories, click-for-details drawer, two-point mileage calculation, and the "Auto-Fed" screenshot ingestion button.
* **Stage 2 — UI Wireframe (`Prototype`):** Sketched the Chicagoland map view, `[Points]` pop-out sidebar, `[Add Point]` screenshot/manual modal, and the 12-field work order detail and technician notes form.
* **Stage 3 — AI-Assisted Iterative Engineering (`index.html`):** Built and refined the live application with **Machine Learning AI Gemini**, adding live OSRM road routing, client-side OCR, FedEx hub workflows, multi-floor building glow detection, and zoom-responsive badge alignment.

---

## ✨ Complete Feature Set (Updated Today)

### 1. 📍 Persistent Pill Pins & Smart Color-Coding Taxonomy
Every pin on the map displays the **last 4 digits of the `WA#` work order number** (and optional `📦 Last 4 FedEx Pkg #`) at all times so technicians can identify stops at a glance:
* 🔴 **Red (`🏠 HOME`):** Default Home Base centered in **North Lawndale (`3600 W 16th St, Chicago, IL 60623`)**, accessible via the **`🏠 Enter Home Base`** button.
* 🟠 **Orange (`📦 HILL` / `📦 DTWN`):** Dedicated FedEx Parts Pickup / Drop locations.
* 🟢 **Blue-to-Green Gradient Pin:** Work order with parts assigned to the **Hillside FedEx Hub**.
* 🟡 **Blue-to-Light-Yellow Gradient Pin:** Work order with parts assigned to the **Downtown FedEx Hub**.
* 🟣 **Animated Purple Gradient Glow (`🏢`):** Automatically triggers when **2 or more work orders share the same street address or building** (even across different floors/suites or slight spelling variations like `St` vs `Street`).
  * **Side-by-Side Pin Fanning:** Multi-floor pins in the same building automatically fan out horizontally so they never overlap on the map.
  * **Coordinated Same-Building + Hub Colors:** Combines the **Purple Same-Building Glow** with the **Hillside Green** or **Downtown Yellow** gradient so both building grouping and FedEx hub assignment are visible simultaneously.

### 2. 📦 One-Click "Fedex Pickup" Popdown Menu & Package Tracking
* **Top-Bar `📦 Fedex Pickup ▾` Dropdown:** Located right next to `🏠 Enter Home Base`, allowing one-click plotting (or removal) of the two primary Chicagoland FedEx Ship Centers:
  * **Hillside:** `300 Craig Pl, Hillside, IL 60162` (`📦 HILL`)
  * **Downtown Chicago:** `1242 S Canal St, Chicago, IL 60607` (`📦 DTWN`)
  * Includes a **`+ Add Both`** quick action and live `✅ On Map` status indicators.
* **Manual FedEx Package # (Last 4 Digits) & Hub Checkboxes:** Inside every Work Order's detail modal, technicians can type the **last 4 digits of the FedEx tracking number** right next to the `Work Order #` and check either **`Hillside (Blue→Green)`** or **`Downtown (Blue→Yellow)`**.

### 3. 🌐 Color-Coded "Overview All (From Home)" & Hover Spotlight
Clicking **`🌐 Overview All (From Home)`** calculates real road routes from the North Lawndale Home Base (`3600 W 16th St`) to every active stop on the map and ranks them **Closest → Farthest**:
* **Color-Coordinated Route Lines:**
  * **Green Line (`#10b981`):** Hillside FedEx Work Order
  * **Gold / Light Yellow Line (`#fde047`):** Downtown FedEx Work Order
  * **Purple Casing + Green/Yellow Inner Line:** Same-Building Work Order coordinated with its Hillside or Downtown FedEx hub
  * **Orange Line (`#f97316`):** FedEx Pickup Location
* **Interactive Category Filter Tabs:** Filter visible map lines and sidebar cards by **`All Lines`**, **`🟢 Hillside`**, **`🟡 Downtown`**, **`🟠 Pickup`**, or **`🟣 Same Building`**.
* **Hover Route Spotlighting:** Hovering over any work order in the Overview panel highlights its specific route line and dims all other lines so dense multi-stop maps are never confusing.

### 4. ⏱️ Stacked Estimated Drive Time + Miles & Zoom-Aware Auto-Alignment
* **Drive Time Above Miles:** Every route badge displays **`⏱️ Estimated Drive Time`** stacked directly above **`🚗 Road Miles`** (e.g., `⏱️ ~13 mins` above `🚗 5.6 mi`), incorporating an urban Chicagoland traffic factor.
* **Zoom-Out Auto-Alignment Engine:** When zooming out on the map, a 2D screen-space collision-avoidance algorithm automatically separates and aligns all mileage/drive-time boxes so they never overlap, drawing a dashed color-coded leader tether back to each route's midpoint.

### 5. 📱 "Auto-Fed" Screenshot OCR Pipeline & Productivity Shortcuts
* **Drag-and-Drop / `Ctrl+V` Screenshot Upload:** Uses client-side **Tesseract.js OCR** and custom Regex token isolation to read WWTS mobile screenshots, capturing the top `WA#` work order number (ignoring adjacent UI icons), scheduled SLA time, site code/ticket #, address, floor/suite, and customer contact fields.
* **One-Click Copy Email (`📋 Copy`):** Copies the customer's email address to the clipboard with instant visual confirmation.
* **Instant Delete + Undo Toast (`Ctrl+Z`):** Every point in the `All Points` drawer includes a quick-delete button below its badge, paired with a pop-up **Undo Toast** and **`Ctrl+Z` / `Cmd+Z`** keyboard shortcut support.
* **Map Style Switcher:** Toggle seamlessly between **Google Maps Road**, **Esri Street**, and **Google Satellite Hybrid** views.

---

## 🛠️ Tech Stack

* **Code Generation & Architecture Partner:** Built with **Machine Learning AI (Google Gemini)**
* **Frontend UI:** HTML5, Tailwind CSS, Vanilla JavaScript (ES6+).
* **Geospatial Mapping & Routing:** Leaflet.js, Google/Esri Tile Layers, OSRM (Open Source Routing Machine) Driving API, ArcGIS + Photon Triple-Fallback Geocoder.
* **Optical Character Recognition (OCR):** Tesseract.js v5 (Client-Side WebAssembly OCR).
* **Persistence:** Browser `localStorage` with 1-Click JSON Export/Import for cross-device sync.

---

## 🚀 Quick Start

1. Clone this repository or download `index.html`. OR go to "https://benjamincristea-1.github.io/wwts-fieldroute-ocr-mapper/" (Github pages)
2. Open `index.html` directly in any modern desktop or mobile web browser (no build step or server installation required).
3. Click **`📦 Fedex Pickup`** to plot the **Hillside** or **Downtown** FedEx hubs, click **`🌐 Overview All (From Home)`** to view color-coded routes and drive times from North Lawndale, or click **`➕ Add Work Order`** to upload/paste a WWTS dispatch screenshot.

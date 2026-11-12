# 3D Model Reference: H. B. Quick's, 17 & 19 Widmore Road

This sheet gathers what we know about the pilot building that is useful for modelling it in Blender and Unity. It comes from `pilot_building_report.ipynb`, the OSM extracts, the 2025 photo, the 1892 advert, the student workbook and the 2025 Conservation Area Appraisal.

Each figure is tagged with how much to trust it:
- **[measured]**: taken from data
- **[photo]**: scaled from `images/19widmore.jpg`, about ±10–15%
- **[inferred]**: typical Victorian practice, not yet checked against this building

---

## 1. Identity

| | |
|---|---|
| Business | **H. B. Quick's**: "Shirtmaker, Tailor, Hatter, Hosier & Outfitter"; sole Bromley & District agent for Dr. Jaeger's Sanitary Wool Clothing and Bedding; "a special department for ladies" |
| Proprietor | Henry Bailey Quick (wife Louisa). Shared the premises with **A. Sussenbach** (tailor & outfitter) in 1892 |
| 1892 address | 9 & 10 Widmore Road (Strong's 1892 p.173) |
| Modern address | **17 & 19 Widmore Road, Bromley BR1 1RL** (modern = 2 × old − 1) |
| Today | 17 = Mozart Barber Shop; 19 = 1917 Chill Café, with 19A offices above (sold at auction in March 2025) |
| Building type | Mid-Victorian two-storey terrace of shops with living space above. Part of the terrace at modern nos. 1–21 on the north side of Widmore Road (CA appraisal §4.55) |

### Decide the target year first
| Year | Shopfronts | Signage |
|---|---|---|
| **1892** | Two businesses: Quick + Sussenbach | Two fascias, or a shared one |
| **1896** (Kelly's p.10, Bush p.204) | Quick holds both units | One "H. B. QUICK'S" business across two fronts |

---

## 2. Location and coordinate system

**Use the notebook's projection everywhere** (`to_m()` in cell 14) so that Blender, Unity and the notebook agree:

```
origin  LAT0 = 51.40619, LON0 = 0.01610   (WGS84)
E = (lon − LON0) · π/180 · 6371000 · cos(LAT0)
N = (lat − LAT0) · π/180 · 6371000
```
- Blender: X = East, Y = North, Z = Up. The glTF exporter converts to Unity's Y-up.
- The building's front-west corner (the west party wall of no. 17 at the street) is at **E 17.99, N −8.91** in this system.

| Orientation | Value |
|---|---|
| Street line (frontage) | runs **10.7° north of east**, compass bearing 79° [measured] |
| Front façade faces | **bearing 169°, roughly south-south-east** [measured] |
| Front façade to Widmore Road centreline | **6.8 m** [measured, OSM way 5730767, 2 lanes, A222]. That leaves a pavement of about **3–3.5 m** after a carriageway of about 6.5 m [inferred] |
| Ground | treat as flat across the site (no elevation data held) |

Sunlight: the front is lit from the south for most of the day, which helps when baking lighting.

---

## 3. Footprints (OSM, © OpenStreetMap contributors, ODbL)

OSM accuracy is about **±0.5–1 m**. The footprints are traced from aerial imagery and are good enough for massing but not for a survey. None of the four ways has height, level or roof tags. All are tagged `building=retail`, and no. 17 also carries `layer=1`.

### 3a. Building-aligned local frame (recommended for Blender)
- Origin: front-west corner of no. 17.
- **u** runs along the frontage, eastward.
- **v** runs perpendicular to it, back into the plot (northward).
- Rotate the finished model by **+10.7° about Z** and move it to (E 17.99, N −8.91) to place it in the shared frame.

| No. (1892) | OSM way | Vertices (u, v) in metres |
|---|---|---|
| **17 (9)** | 961975151 | (0.00, 0.00) · (6.18, 0.04) · (6.40, 18.46) · (2.28, 18.48) · (2.19, 10.97) · (0.45, 10.87) |
| **19 (10)** | 961975152 | (6.18, 0.04) · (12.72, 0.00) · (12.97, 20.47) · (6.42, 20.54) · (6.40, 18.46) |
| 15 (8), neighbour W | 961975150 | (−6.47, 0.43) · (0.00, 0.00) · (0.45, 10.87) · (1.65, 42.04) · (−5.79, 42.00) · (−5.93, 29.50) |
| 21 (11), neighbour E | 961975153 | (12.72, 0.00) · (19.66, 0.32) · (19.94, 13.74) · (19.90, 14.84) · (16.98, 14.79) · (17.15, 28.64) · (15.03, 28.67) · (15.01, 26.95) · (13.05, 26.98) · (12.97, 20.47) |

### 3b. Same vertices in the shared E/N frame (metres)
| No. | Vertices (E, N) |
|---|---|
| 17 | (17.99, −8.91) · (24.06, −7.73) · (20.85, 10.42) · (16.81, 9.67) · (18.11, 2.28) · (16.41, 1.86) |
| 19 | (24.06, −7.73) · (30.49, −6.55) · (26.94, 13.61) · (20.49, 12.46) · (20.85, 10.42) |
| 15 | (11.56, −9.69) · (17.99, −8.91) · (16.41, 1.86) · (11.81, 32.70) · (4.51, 31.29) · (6.69, 18.98) |
| 21 | (30.49, −6.55) · (37.25, −4.95) · (35.04, 8.30) · (34.79, 9.36) · (31.93, 8.77) · (29.53, 22.42) · (27.44, 22.05) · (27.74, 20.36) · (25.81, 20.03) · (26.94, 13.61) |

The raw lat/lon values are in `data/osm_buildings_extract.json`.

### 3c. Plan dimensions
| | No. 17 | No. 19 | Both |
|---|---|---|---|
| Frontage | **6.18 m** | **6.54 m** | **12.72 m** |
| Total depth (OSM) | 18.5 m | 20.5 m | |
| Area (OSM) | 96.7 m² | 134.2 m² | |

**How to read the shapes:**
- **No. 17** has a full-width **main range about 10.9 m deep**, plus a narrower **rear wing about 4.1 m wide** (u 2.2–6.4) running from v 10.9 to 18.5 along the party wall with 19. This is the usual Victorian layout of main range plus back addition [inferred]. The open strip behind the main range (u 0–2.2) would have been a yard.
- **No. 19** is mapped as one rectangle 20.5 m deep. It most likely combines the same ~11 m main range with a later rear extension [inferred]. Model the front ~11 m in detail and the rest as low-detail massing.
- The OSM polygons include rear additions, so the **OSM depth is an upper bound** for the 1890s building.

---

## 4. Front elevation (scaled from the 2025 photo)

**Scale:** no. 19 spans photo x = 330 → 765 px across 6.54 m, which gives **66.5 px/m**. A brick-course check agrees: courses repeat about every 5 px, which is 75 mm per course at that scale, so the vertical scale matches the horizontal. Pavement level is at photo y ≈ 690.

### 4a. Heights above pavement
| Element | Height | Note |
|---|---|---|
| Stallriser top (no. 17, original front) | ~0.40 m | [photo] |
| Shop glazing top / transom line | ~2.5 m | [photo] |
| Blind (awning) box | ~2.9–3.2 m | [photo] |
| Fascia + shop cornice | ~3.2–4.2 m (fascia ~0.85 m deep) | [photo] |
| First-floor window sills | ~4.25 m (sitting right on the shop cornice) | [photo] |
| First-floor window heads | ~5.6 m | [photo] |
| Window lintels | ~5.7–6.0 m (≈0.28 m deep, ≈1.4 m wide) | [photo] |
| Top of front brickwork | ~6.1 m | [photo] |
| **Eaves / gutter line** | **~6.3–6.5 m** | [photo] |
| Visible ridge line | ≥7.6 m apparent | foreshortened; the true ridge is probably **8–9 m** [inferred] |
| Chimney stack top (17/19 party wall) | ~8.9 m, pots to ~9.3 m | apparent; set back, so probably slightly taller [photo] |

### 4b. First floor (both shops, symmetric)
- **Two windows per shop**, about **1.0 m wide × 1.35 m high** [photo]. The current windows are modern uPVC replacements. The originals were probably timber sashes, and possibly taller [inferred]. Check this on site.
- No. 19 window positions from its west party wall: **1.5–2.5 m** and **4.0–5.0 m**. That leaves about 1.5 m of brick at each end and about 1.5 m between the windows. Use no. 19 as the template for no. 17.
- Plain flat **pale lintels** (painted stone or stucco), about 1.4 m wide. There are no visible sill bands or string courses.
- Wall: **yellow London stock brick**. The bond looks like Flemish (alternating headers and stretchers); confirm on site.
- Eaves: a projecting dark eaves or gutter band about 0.3–0.4 m deep, continuous along the terrace.

### 4c. Roof
- **Pitched slate roof** with the ridge parallel to the street, continuous along the terrace [photo + CA appraisal].
- **Coped brick party-wall parapets** rise above the roof slope at both party walls of 19 [photo]. Keep them; they are probably original.
- A **brick chimney stack** with pots sits on the 17/19 party wall [photo]. There are more stacks along the terrace (21/23 has red pots).
- Roof pitch is not measurable from the photo. Use **about 35–40°** as a placeholder [inferred].
- **Leave out** the modern dormers (one centred on 19, others on 17 and 21).

### 4d. Ground floor (shopfronts)
**No. 17: original Victorian shopfront.** Use it as the template for both shops.
- The CA appraisal (§4.55) describes it: *"ornate shopfront with carved colonettes and mirrored soffit above the recessed door."*
- A **central recessed entrance** with splayed display windows on either side. The door is centred on the 6.18 m frontage.
- Slim white **colonettes** (mullions) divide the glazing, and a low **stallriser** (~0.4 m) runs underneath.
- **Pilasters** at each party wall carry the **fascia and cornice** (about 3.2–4.2 m).
- A separate narrow **door to the upper floor** at the east end next to the pilaster (now 17A). It is partly hidden in the photo.
- The modern awning hides the mirrored soffit. Photograph it in person.

**No. 19: modern front.** Rebuild it from the no. 17 pattern.
- Today it has a central door (~0.85 m) between multi-pane windows, plus a **separate ~1.0 m door to the upper floors (19A)** at the east end.
- The 19A side-door bay is probably original in arrangement, since it mirrors 17A [inferred].
- For **1896**, use a matching pair of fronts under one continuous "H. B. QUICK'S" fascia. For **1892**, use two fascias.

### 4e. Modern items to leave out
Dormers, uPVC windows, awnings, modern fascias and signs, the burglar alarm, CCTV, cabling, the satellite or utility boxes, the downpipe at the 17/19 party wall (it may replace an original cast-iron pipe), and the café and barber fit-outs.

---

## 5. Signage and graphic material

**Source:** `images/Quick.png` (Strong's Directory 1892 advert, 990 × 740 px), Prof. Bilston's Shortlands gallery.

Advert wording for the fascia and window bills:
```
H. B. QUICK'S
Shirtmaker, Tailor, Hatter, Hosier & Outfitter
9 & 10, WIDMORE ROAD
Dr. JAEGER'S SANITARY WOOL CLOTHING and BEDDING
SOLE AGENT FOR BROMLEY AND DISTRICT
A SPECIAL DEPARTMENT FOR LADIES
"Wool, all Wool; Nothing but Wool; Wool all the year round."
```
- Lettering in the advert:
  - "H. B. QUICK'S": heavy slab/Clarendon-style display capitals
  - Trade line: condensed serif
  - "Jaeger's": bold Roman
  - "Sanitary Wool…": decorative blackletter-style face

  For a painted fascia, use gilt or cream serif capitals on a dark ground, which is typical for the period [inferred].
- The Jaeger product ad (`images/1907-JaegerSpecialPureWoolUnderwear-500.jpeg`) can be used for window-display bills and props. It is dated 1907, so use it only as a style reference for an 1890s scene.
- Workbook image links:
  - 9 Widmore Road: the Quick advert and two Jaeger sources (Cincinnati & Hamilton County Public Library; Gjenvick Archives)
  - 11 Widmore Road (Dyer, next door): `.../1892-strongs-directory/Dyer.png`. This is useful for the neighbour's sign.

---

## 6. Street context (1892 occupants, for neighbouring blocks)

| 1892 no. | Modern no. | Occupant | Model at |
|---|---|---|---|
| 8 | 15 | Turner, Oil & Colourmen | massing + matching terrace façade |
| **9 & 10** | **17 & 19** | **H. B. Quick (+ A. Sussenbach in 1892)** | **hero / full detail** |
| 11 | 21 | Thomas Dyer, Cinderella Boot Stores (uninhabited by 1901) | massing + matching terrace façade |
| 12–13 | 23–25 | H. G. Cooper, butcher | optional; not covered by the CA terrace description |

The terrace from 1 to 21 shares its height, materials and window rhythm, so **one modular kit covers every neighbour**: a 6–7 m bay with two upper windows, a shopfront, a party parapet and a chimney.

---

## 7. Interior (only if needed)

There is no direct evidence for the interior. Use period practice [inferred]:
- **Ground floor:** shop with counter, glazed cases and shelving for shirts, hats and hosiery. There is a "ladies' department", possibly the second unit after 1896.
- **First floor:** living accommodation or workroom.

The Quicks lived at 81 Widmore Road by 1901, so by then the space above may have been let or used for storage.

---

## 8. What is still missing (in order of priority)

1. **Measured heights and roof pitch.** Measure on site with a laser measure, or build a photogrammetry scan of 15–21. These replace every [photo] estimate above.
2. **Close-up photos of the no. 17 shopfront**: colonettes, mirrored soffit, recessed door, fascia mouldings, stallriser. This is the only original detail we have.
3. **1890s Ordnance Survey 1:500 or 1:2500 map or a Goad insurance plan**, to confirm the original depth, the rear wings and the yards.
4. **Historic photo of the Widmore Road north side** (BBLHS, Bromley Historic Collections), for original windows, colours, blinds and signage.
5. **Post-1902 directory entry**, to confirm Quick at 17 & 19 under the new numbering (the open item in the notebook).
6. Rear elevation: no data. Keep it simple.

---

## Source files
- `pilot_building_report.ipynb`: §5–8
- `data/osm_buildings_extract.json`: ways 961975150–153
- `data/osm_widmore_road_addresses_extract.json`: shop points, road way 5730767
- `images/19widmore.jpg`: 2025 elevation photo (Auction House London, Lot 38)
- `images/Quick.png`: 1892 advert; `images/1907-JaegerSpecialPureWoolUnderwear-500.jpeg`
- `sources/conservation_area_appraisal_2025_text.txt`: §4.54–4.56, §5.19–5.21
- `data/Downtown Bromley - Directory Info - 2026-06-02.xlsx`: rows for 8–11 Widmore Road

# Pilot Building Selection Report

This folder explains why **H. B. Quick's tailor & outfitter** was chosen as the pilot building for the Virtual Victorian December demo. In 1892 it was 9 & 10 Widmore Road; today it is 17 & 19 Widmore Road, Bromley BR1 1RL.

Open `pilot_building_report.ipynb` and run it from top to bottom.

## Folder contents

```
pilot_building_report/
├── pilot_building_report.ipynb   ← the report
├── data/
│   ├── Downtown Bromley - Directory Info - 2026-06-02.xlsx   (student workbook)
│   ├── osm_buildings_extract.json                            (OpenStreetMap footprints)
│   └── osm_widmore_road_addresses_extract.json               (OpenStreetMap shop points)
├── images/    2025 street photo, 1892 Quick advert, Jaeger advert, Collins advert
└── sources/   Bromley Town Centre Conservation Area Appraisal 2025 (PDF + extracted text)
```

## How the building was chosen

1. **Scoring:** every address in the workbook was scored by its number of filled evidence fields (directory page refs, census fields, image links).
2. **Combining shops:** businesses spread over two plots were combined. Quick (9 + 10) scores **15**, Cooper (12 + 13) **13**, and Collins (17) **12**.
3. **Renumbering:** Widmore Road was renumbered after 1892 (modern = 2 × old − 1). This was tested against the 1901 census notes.
4. **Survival:** each candidate's modern number was checked against Bromley Council's 2025 appraisal. Quick's building survives, with an original shopfront at no. 17. Collins's building was demolished, and Cooper's isn't covered by the appraisal.
5. **Location:** the building was confirmed with OpenStreetMap footprints and a 2025 photo.

## Requirements

Python with pandas, numpy, matplotlib and openpyxl. 

OpenStreetMap data © OpenStreetMap contributors (ODbL).

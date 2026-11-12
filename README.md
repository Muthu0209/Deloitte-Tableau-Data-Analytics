# Deliotte-Tableau-Data-Analytics
Deloitte Australia Data Analytics Job Simulation (via Forage): built a Tableau dashboard analyzing Daikibo factory telemetry data to identify machine downtime by location and device type, and completed a forensic pay-equity analysis classifying gender pay equality scores across job roles and factories.

## Task 1: Telemetry Dashboard (Tableau)

### Business questions

1. In which location did machines break the most?
2. Which machines broke most often in that location?

### Data

- One month (May 2021) of telemetry in a single JSON file (`daikibo-telemetry-data.json`), included in this repo as `daikibo-telemetry-data.json.zip`.
- 4 factories, 9 machine types each, each machine sending a status message every 10 minutes.

| Factory | Location |
|---|---|
| Daikibo Factory Meiyo | Tokyo, Japan |
| Daikibo Factory Seiko | Osaka, Japan |
| Daikibo Berlin | Berlin, Germany |
| Daikibo Shenzhen | Shenzhen, China |

### Approach

1. Imported the JSON into Tableau with all schema levels selected.
2. Created a calculated measure, **Unhealthy**: `IF [status]="unhealthy" THEN 10 ELSE 0 END`. Each unhealthy message represents 10 minutes of potential downtime, so downtime figures below are estimates.
3. Built the bar chart **Down Time per Factory**.
4. Built a second sheet with the bar chart **Down Time per Device Type**.
5. Combined both into a dashboard, with the factory chart acting as a filter for the device chart.

### Findings

- **Daikibo Factory Seiko (Osaka)** had the most downtime, at an estimated **480 minutes**.
- Shenzhen was second, Meiyo third, and Berlin had by far the least.
- Within Seiko, the **LaserWelder** was the machine responsible for essentially all of the downtime.

### Dashboard

![Dashboard](<Muthulakshmi Viswanathan- Dashboard Image.png>)

### Deliverables

- `Deliotte tableau.twb`: the Tableau workbook
- `Muthulakshmi Viswanathan- Dashboard Image`: dashboard screenshot

---

## Task 2: Forensic Technology, Gender Pay Equality (Excel)

### Background

After internal complaints about gender pay inequality, Daikibo's Forensic Tech team built an algorithm that produces an **Equality Score** (integer from -100 to +100, where 0 is ideal) for each job role at each factory.

### Task

Add a fourth column, **Equality class**, that classifies each score:

| Class | Rule |
|---|---|
| Fair | -10 ≤ score ≤ +10 |
| Unfair | -20 ≤ score < -10, or +10 < score ≤ +20 |
| Highly Discriminative | score < -20 or score > +20 |

### Approach

Used a nested Excel formula (shown for row 2):

```excel
=IF(AND(C2>=-10,C2<=10),"Fair",IF(OR(C2<-20,C2>20),"Highly Discriminative","Unfair"))
```

### Results (37 factory and job role combinations)

| Class | Count |
|---|---|
| Fair | 19 |
| Unfair | 11 |
| Highly Discriminative | 7 |

| Factory | Fair | Unfair | Highly Discriminative |
|---|---|---|---|
| Meiyo | 4 | 4 | 3 |
| Seiko | 5 | 2 | 3 |
| Berlin | 5 | 3 | 0 |
| Shenzhen | 5 | 2 | 1 |

Both Japanese factories show the most severe pay inequality (3 highly discriminative roles each), while Berlin has none.

### Deliverable

- `Task 5 Equality Table.xlsx`: the completed table with the classification column (labeled "Task 5" in the original Forage module, and it is Task 2 in this README)

---

## Skills Demonstrated

- Data import and transformation from JSON
- Calculated fields and dashboard interactivity in Tableau
- Conditional logic in Excel (`IF`, `AND`, `OR`)
- Turning data into business insight and clear communication

## Repository Contents

| File | Description |
|---|---|
| `Deliotte tableau.twb` | Tableau workbook (Task 1) |
| `Muthulakshmi Viswanathan- Dashboard Image` | Dashboard screenshot (Task 1) |
| `daikibo-telemetry-data.json.zip` | Zipped source telemetry data, May 2021 (Task 1) |
| `Task 5 Equality Table.xlsx` | Pay-equity classification (Task 2) |
| `Deloitte Data Analysis certificate.pdf` | Forage completion certificate |

## How to Open

- Open the `.twb` in [Tableau Desktop](https://www.tableau.com/products/desktop) or Tableau Public. The telemetry data is included as `daikibo-telemetry-data.json.zip`. Unzip it first, then point Tableau to the extracted `daikibo-telemetry-data.json` if prompted.
- Open the `.xlsx` in Excel or Google Sheets.

## Credits

Simulation provided by Deloitte Australia via Forage. All company data is fictional.


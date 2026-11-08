# prepaid-plan-automation-a360
RPA bot in Automation Anywhere A360 that scrapes prepaid plan data (price, data, validity) from a telecom website into Excel.

# Prepaid Plan Data Automation (Automation Anywhere A360)

An RPA bot built with **Automation Anywhere A360** that scrapes prepaid recharge plan details (price, data benefit, validity) from the Vi India website and writes them into an Excel sheet automatically.

> **Context:** I participated in the *AI Hackathon for Builders* (organised by GL Bajaj Institute of Management and Research on Unstop) and received a Certificate of Participation. This automation is a separate project I built in A360 to explore how automation and AI can solve real business problems.

---

## Business Problem

Telecom operators change prepaid plan prices, data benefits and validity often. Analysts who compare plans usually:

- copy plan details from the operator website into Excel by hand,
- spend time on repetitive work that does not scale,
- risk copy-paste errors and outdated data.

## Solution

A bot that opens the Vi recharge page, loops through every plan on the page, extracts the three key fields and writes each plan as a row in `VI.xlsx`.

| Column | Field |
|--------|-------|
| A | Price |
| B | Data benefit |
| C | Validity |

## How It Works (Workflow)

1. **Browser: Open** the Vi prepaid recharge page in Microsoft Edge.
2. **Excel advanced: Open** the output workbook (`VI.xlsx`).
3. **Loop** while the plan label exists on the page.
4. **Recorder: Capture** (HTML InnerText) the plan label, price/data and validity.
5. **Message box** to display the captured values (used for debugging).
6. **Excel advanced: Set cell** writes price, data and validity into columns A, B and C of the current row.
7. **Number: Increment** the row counter (`SetCell`) and loop counter (`numCounter`).

### Variables used

| Variable | Type | Purpose |
|----------|------|---------|
| `strRs` | String | Plan price |
| `strGbdata` | String | Data benefit |
| `strValadity` | String | Validity |
| `SetCell` | Number | Current Excel row |
| `numCounter` | Number | Loop counter |

## Screenshots

### A360 workflow
![Workflow](<img width="1365" height="681" alt="Screenshot 2026-11-08 145324" src="https://github.com/user-attachments/assets/3e17b0c9-86ab-4093-abd6-760079b3f2c2" />
)

### Excel output
![Excel output](<img width="1365" height="767" alt="Screenshot 2026-11-08 150458" src="https://github.com/user-attachments/assets/c5b3f886-805a-47c7-a576-ab11a73ddea4" />
)

## Tech Stack

- Automation Anywhere A360 (Community Edition)
- Actions: Browser, Recorder, Loop, Excel advanced, Number, Message box
- Microsoft Edge, Microsoft Excel
- Windows

## Prerequisites

- An A360 account (Community Edition is free) and the Bot Agent installed (Browser: Open requires bot agent version 21.210 or above)
- Microsoft Edge with the A360 browser extension installed
- Microsoft Excel installed

## How to Run

1. Import the bot into your A360 Control Room (see `bot/`).
2. Create an empty `VI.xlsx` with headers `Price`, `Data`, `Validity` in row 1.
3. Open the bot and update the Excel path in the **Excel advanced: Open** step to your own file location.
4. Set the starting row variable (`SetCell`) to `2`.
5. Click **Run**.

## Results

The bot extracted 20+ plans in a single run, with validities ranging from 28 days to 365 days. See `output/VI.xlsx` for a sample output.

## Known Limitations

- Some **Data** values are truncated (for example "/day"), because the captured element does not contain the full benefit text.
- The bot depends on the website's current layout. If Vi changes its page, the captured objects may need to be re-recorded.
- File paths are currently local to my machine and must be changed to run elsewhere.

## Future Improvements

- Improve selectors and add a cleanup step for the Data column.
- Extend to Airtel and Jio for side-by-side plan comparison.
- Schedule the bot to track plan price changes over time.
- Add AI to recommend the best plan for a user's needs.

## Repository Structure

```
prepaid-plan-automation-a360/
|-- README.md
|-- bot/                     # exported A360 bot (.zip)
|-- output/
|   `-- VI.xlsx              # sample output
|-- docs/
|   |-- images/
|   |   |-- workflow.png
|   |   `-- excel-output.png
|   `-- A360_Plan_Automation_Project.pptx
`-- .gitignore
```

## Disclaimer

Built for learning and demonstration. Plan data belongs to the respective operator. Please follow the website's terms of service and avoid heavy or repeated automated requests.

## Author

**Faisal Mohsin** - Jamia Hamdard, New Delhi

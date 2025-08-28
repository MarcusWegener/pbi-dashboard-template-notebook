# Portable Power BI Dashboard Templates with Fabric Notebooks (PoC)

> **Goal**: Make Power BI dashboards **portable** by parameterizing field bindings so a template can be redeployed to a **different semantic model** with minimal manual work.

![Deploy Monitoring Dashboard](Deploy_Monitoring_Dashboard.gif)

---

## Why this matters
Power BI report definitions often contain **hard-coded** bindings (tables, columns, measures). Reusing a great dashboard across workspaces or customers becomes manual and brittle.  
This Proof of Concept shows how a Fabric Notebook can **re-bind** those references programmatically using `semPy`, enabling a reusable **dashboard catalog** / **dashboard factory** pattern.

---

## What’s inside
- A Fabric Notebook that:
  - loads a reference **template** report,
  - applies **parameterized mappings** from placeholders → target semantic model,
  - updates the report definition via `semPy`,
  - and lets you validate the result in seconds.
- Minimal demo configuration; **no sensitive data** required.

> This PoC builds on the public reference model and template in this repository.

---

## Quick Start (Fabric)
1. **Upload the notebook** to a **Fabric workspace** backed by Fabric capacity.  
2. In the notebook’s **configuration section**, set the following variables to match your **target semantic model**:
   - `workspace_id` – GUID of the Fabric workspace containing the target model  
   - `dataset_id` – GUID of the target **semantic model** (Power BI dataset)  
   - `act_measure` – name of the **Actuals** measure to bind (e.g., `Sales Amount`)  
   - `bud_measure` – name of the **Budget** measure to bind (e.g., `Budget Amount`)  
   - `dimension` – dimension column used in visuals (e.g., `Customer.Name`)  
   - `report_name_override` – optional new report name for the deployed copy  
3. **Run** the notebook.  
4. **Open the generated report** → check the loaded **Monitoring Dashboard** and enjoy 😊

> Tip: Keep a small **mapping registry** (CSV/JSON) if you deploy the template to many models. It improves repeatability and reviewability.

---

## Prerequisites
- Fabric capacity (trial or paid) and a workspace in Fabric
- **Contributor** (or higher) on the workspace
- **Build permission** on the target semantic model
- Python in notebooks is **Preview**; PySpark is **GA**
- `semPy` enabled
- The semantic model name must **not** end with a space

---

## Design Notes & Caveats
- **Visual Calculations** can keep logic close to visuals, reducing coupling to the model and improving portability.
- **Report-specific measures** are possible. For parametrization, define a dedicated **home table** for report measures.
- The `visual.json` references a **home table** for measures; therefore, placeholders in the template must be **unique and consistent** to support multiple home tables.
- This is a **Proof of Concept**. Expect to extend the mapping logic for broader coverage (e.g., custom visuals with special bindings).

---

## Credits
- Patrick LeBlanc: *Creative way to use semPy to update a Power BI report definition*  
  https://youtu.be/HT_J1QiBLwA?si=MpxYYYWvGIBtUhTM
- Fabric Unified Admin Monitoring (FUAM)  
  https://github.com/microsoft/fabric-toolbox/tree/main/monitoring/fabric-unified-admin-monitoring

---

## Publication & Acknowledgments
- This Proof of Concept was developed **with the assistance of ChatGPT**.
- Published as part of the **Fabric Notebooks for Power BI – August Contest**.  
  Contest announcement: https://community.fabric.microsoft.com/t5/Power-BI-Community-Blog/Fabric-Notebooks-for-Power-BI-August-Contest/ba-p/4785694

---

## ⚠️ Disclaimer
This notebook is provided **as-is** for demonstration purposes only.  
Use at your own risk; **no liability** is assumed for any damages arising from its use.

---

## Contributing
Issues and PRs welcome. If you extend the mapping logic or add test datasets, please include a short note in the README so others can reproduce your results.

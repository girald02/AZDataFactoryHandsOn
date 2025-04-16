# 🚀 Azure Data Factory in Action: Ingesting Raw Files and Executing Data Transformations in Real-Time Scenarios

This project is a hands-on implementation of a **real-time data orchestration scenario** using **Azure Data Factory (ADF)**. It demonstrates how to filter and transfer raw `.csv` files from a source folder to a reporting folder — with logic to only pick files starting with `"Facts"`.

---

## 📘 Scenario Overview

> ✅ **Objective**: Automatically move only the `"Facts"` raw files from the source folder to the destination reporting folder, used by data analysts.

We use ADF features like metadata inspection, conditional logic, and looping to dynamically filter and transfer files.

---

## 🧱 ADF Resources Used

- **Pipelines**
- **Datasets**
- **Linked Services**
- **Data Flows**
- **Triggers** (manual and storage event-based)
- **Variables**
- **Activities**: `Get Metadata`, `If Condition`, `Foreach`, `Copy Data`, `Delete`

---

## 🔁 Copy Activity Logic

1. **Get Metadata**  
   Retrieves all file names in the source folder using:

@activity('GetMetadata').output.childItems


2. **Foreach Activity**  
Iterates through each file with `item().name`

3. **If Condition Activity**  
Checks if file name starts with `"Facts"`

4. **Copy Activity**  
If condition is true, file is transferred to the reporting folder.

5. **Delete Activity (Optional)**  
Deletes the original file after successful copy.

---

## 🧩 Variables

- `var_files` (Array)  
Used to store the list of files retrieved from metadata.

---

## 🔄 Data Flow: Data Transformation

After files are moved, a Data Flow can process the data for reporting:

**Flow Diagram:**

sourceCSV → SelectCol → Filter Rows (row != 12) → Conditional Split (MasterCard, Visa, etc.) → Derived Column (e.g., coalesce nulls) → Aggregate (group by max) → Sink (write to output)


### Components:
- **SelectCol**: Keep only necessary columns  
- **Filter Rows**: Exclude unwanted rows  
- **Conditional Split**: Split based on card type  
- **Derived Column**: Transform or add new fields  
- **Aggregate**: Group data for summaries  
- **Alter Rows**: Keep only valid records  
- **Sink**: Final destination of processed data

---

## 📅 Triggers

### Scheduled Trigger:
- Go to Pipeline → Add Trigger → New  
- Define schedule and run time

### Storage Event Trigger:
- Automatically trigger pipeline when new files arrive in blob storage

#### Setup:
- **Container name:** `source`  
- **Blob path begins with:** (e.g., `raw/`)  
- **Blob path ends with:** `.csv`  
- **Azure Setup:**  
  - Go to **Azure Portal → Subscriptions → Resource Providers**  
  - Register: `Microsoft.EventGrid`

---

## ✅ Summary

This project covers a practical use case of:
- Using ADF to filter files dynamically  
- Automating transfers based on conditions  
- Running transformations with Data Flows  
- Triggering pipelines via schedules or blob events

---


## 📌 Technologies

- Azure Data Factory  
- Azure Blob Storage  
- Manual and Automated Triggers
- Data Flows

---

## 📬 Contact
For questions or collaborations:  
**📧 Email:** rare.girald@gmail.com
**🔗 LinkedIn:** https://www.linkedin.com/in/girald-bacongan-988144174/




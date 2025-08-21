# 📊 CSV Chart Generator via Dify ChatFlow

A locally deployed ChatFlow built with [Dify](https://dify.ai/) that transforms CSV files into structured JSON and generates charts using a large language model. Ideal for data beginners, educators, and AI workflow enthusiasts.

---

## ✨ Features

- Upload a CSV file with two columns (e.g., name + value)
- Automatically converts CSV to JSON format
- Outputs structured data for chart generation (e.g., bar chart, line chart)
- Powered by DeepSeek Chat for intelligent parsing
- Fully local—no internet required

---

## 📁 Sample Input

**CSV file:**
Fruit,Quantity Apple,10 Banana,12 Lychee,15 Pear,13


**Converted JSON:**
```json
{
  "name": ["《Apple》", "《Banana》", "《Lychee》", "《Pear》"],
  "values": [10, 12, 15, 13]
}
```

## 🧠 Workflow Overview

```mermaid
graph TD
    A[📥 CSV Upload] --> B[🧠 Parameter Extractor]
    B --> C[🧾 LLM Parsing]
    C --> D[📦 JSON Formatter]
    D --> E[📊 Chart Generator]

<img width="1050" height="718" alt="image" src="https://github.com/user-attachments/assets/10063c0c-b37b-4106-9d3d-11f7438de778" />

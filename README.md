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

## 🧠 Workflow Overview
graph TD
    A[CSV Upload] --> B[Parameter Extractor]
    B --> C[LLM Parsing]
    C --> D[JSON Formatter]
    D --> E[Chart Generator]
<img width="1050" height="718" alt="image" src="https://github.com/user-attachments/assets/10063c0c-b37b-4106-9d3d-11f7438de778" />

### 代码执行部分：
import json
import re

def main(jsonData: str) -> dict:
    # 去除换行符和制表符
    clean_str = re.sub(r'[\n\t]', '', jsonData)

    # 修正：去除转义的双引号（将\"替换为"）
    clean_str = re.sub(r'\\"', '"', clean_str)

    # 修正：提取name和values的值（修正正则表达式）
    name_pattern = r'"name":\s*

\[(.*?)\]

'
    values_pattern = r'"values":\s*

\[(.*?)\]

'

    name_match = re.search(name_pattern, clean_str)
    values_match = re.search(values_pattern, clean_str)

    names = []
    if name_match:
        # 修正：正确提取name数组内容
        names = re.findall(r'"([^"]*)"', name_match.group(1))

    values = []
    if values_match:
        # 修正：正确处理values数组
        values = [float(num.strip()) for num in values_match.group(1).split(',')]

    option = {
        "xAxis": {
            "type": 'category',
            "data": names
        },
        "yAxis": {
            "type": 'value'
        },
        "series": [{
            "data": values,
            "type": 'bar',
            "showBackground": True,
            "backgroundStyle": {
                "color": 'rgba(180, 180, 180, 0.2)'
            }
        }]
    }

    # 生成输出文件
    output = f"```echarts\n{json.dumps(option, ensure_ascii=False)}\n```"
    return {
        "result": output,
    }


[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23572450&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.vinhkq@vinuni.edu.vn
**Name:** Khương Quang Vinh

---

## Mo ta

bài lab muốn sinh viên dùng ETL để xử lý raw data trước tạo ra data clean sau đó so sánh kết quả agent trả về với clean data và trash data

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Mo ta cach ban chay thi nghiem Clean vs Garbage data
```
- b1: chay solution.py để tạo clean data
- b2: chạy generate_garbage.py để tạo garbage data
- b3: chạy agent_simulation.py để chạy simulation 


---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua
==================================================
ETL Pipeline Started...
==================================================
Extracting data from raw_data.json...
Extracted 5 raw records.
  [DROP] Record id=3 — invalid price: -10
  [DROP] Record id=4 — empty category
Validation complete. Valid: 3 kept, 2 dropped/errors found.
Transform complete. 3 records processed.
Data saved to processed_data.csv
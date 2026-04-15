[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573948&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 
**Name:** Trương Hầu Minh Kiể

---

## Mo ta

Bai lab xay dung mot ETL Pipeline tu dong doc du lieu JSON, kiem tra chat luong, ap dung business logic (giam gia 10%), va luu ket qua ra CSV. Pipeline duoc thiet ke voi structured logging de quan sat trang thai tung buoc. Sau do, thi nghiem Stress Test so sanh hieu suat cua AI Agent khi xu ly du lieu sach vs du lieu "nhiem doc" (garbage data).

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
python generate_garbage.py
python agent_simulation.py
```

### Chay Tests (Autograder)
```bash
pytest tests/test_autograder.py -v
---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script (extract, validate, transform, load)
├── generate_garbage.py      # Script tao du lieu "nhiem doc" de test
├── agent_simulation.py      # Agent gia lap kiem tra anh huong cua data quality
├── raw_data.json            # Du lieu nguon (5 san pham, 2 bi loai)
├── processed_data.csv       # Output cua pipeline (3 records hop le)
├── garbage_data.csv         # Du lieu "doc" (duoc tao boi generate_garbage.py)
├── experiment_report.md     # Bao cao thi nghiem Clean vs Garbage
└── README.md                # File nay
```

---

## Ket qua

Pipeline xu ly **5 records** tu `raw_data.json`:
- **3 records** hop le duoc giu lai va luu vao `processed_data.csv`
- **2 records** bi loai: id=3 (price=-10) va id=4 (category rong)
- Tat ca records hop le duoc ap dung giam gia 10% va chuan hoa category sang Title Case
- Moi record duoc gan timestamp `processed_at` de truy vet

| id | product | price | category | discounted_price |
|----|---------|-------|----------|-----------------|
| 1  | Laptop  | 1200  | Electronics | 1080.0 |
| 2  | Chair   | 45    | Furniture   | 40.5  |
| 5  | Monitor | 300   | Electronics | 270.0 |

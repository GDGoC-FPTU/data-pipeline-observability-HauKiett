# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600502
**Name:** Trương Hầu Minh Kiệt
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "the best choice is Laptop at $1200" | 9 | Correct — Laptop is the highest-priced valid electronic |
| Garbage Data (`garbage_data.csv`) | "the best choice is Nuclear Reactor at $999999" | 1 | Wrong — extreme outlier ($999,999) skewed the result completely |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi su dung garbage_data.csv, Agent dua ra ket qua sai vi du lieu dau vao chua nhieu loi chat luong nghiem trong.
Cu the, co bon van de chinh da gay ra su co nay:

**Duplicate IDs:** Ban ghi id=1 xuat hien hai lan (Laptop va Banana). Dieu nay co the gay ra nhap nhem trong viec truy vet nguon goc du lieu va lam cho cac phep tinh tong hop bi sai.

**Wrong Data Types:** San pham "Broken Chair" co gia la chuoi "ten dollars" thay vi so. Neu Agent hoac pipeline khong xu ly loi nay, no co the gay ra loi runtime hoac bi bo qua mot cach im lang, khien ket qua thieu chinh xac.

**Extreme Outlier:** Day la nguyen nhan truc tiep gay ra cau tra loi sai. "Nuclear Reactor" co gia $999,999 — mot gia tri bat thuong hoan toan. Voi du lieu sach, gia cao nhat la $1,200 (Laptop), day la con so hop ly. Nhung outlier nay da "chiem quyen uu tien" va Agent bao cao no la "best choice" — mot ket qua vo nghia va co hai.

**Null Values:** Ban ghi co id=None, gia=0, va category=None. Nhung gia tri null nay co the gay ra loi khi Agent co truy cap thuoc tinh, hoac lam nhiez loan logic loc du lieu.

Ket luan: garbage in, garbage out. Agent chi thong minh bang du lieu ma no duoc cung cap. Mot prompt tot hay mot model tot khong the bu dap cho du lieu kem chat luong.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** **Dong y hoan toan.**

Thi nghiem nay cho thay ro rang rang: du ban co mot AI Agent duoc thiet ke tot den dau, neu du lieu dau vao chua loi (outliers, nulls, wrong types, duplicates), ket qua dau ra se sai hoac vo nghia. Mot ETL pipeline manh voi buoc Validate nghiem ngat la lop bao ve dau tien va quan trong nhat truoc khi bat ky AI nao cham vao du lieu. Data quality khong phai la buoc tuy chon — no la nen tang cua moi he thong AI dang tin cay.

## Object Storage: MinIO

Self-hosted S3-compatible object storage สำหรับเก็บ raw และ processed data ทุก layer
ของ pipeline (Landing, Bronze, Silver, Gold)

- **Mode:** Standalone
- **เหตุผลที่เลือก:** S3-compatible API ทำให้ migrate ขึ้น cloud ได้โดยไม่ต้องแก้ code,
  ecosystem กว้าง, ตั้งง่ายบน Kubernetes
- **Deployment:** Helm chart บน Minikube


## Process Engine: DuckDB

In-process OLAP engine สำหรับ transform และ process data ทุก layer ของ pipeline

- **เหตุผลที่เลือก:** Lightweight, S3/MinIO native, multi-threaded, SQL-first,
  ไม่ต้องการ dedicated server — รันเป็น library ใน Python process
- **Deployment:** รันภายใน Pipeline Pod ผ่าน orchestration layer
- **ข้อจำกัด:** Single-node เท่านั้น, เหมาะกับ data ระดับ GB–low TB


## Orchestrator: Dagster

Asset-based pipeline orchestration สำหรับ schedule, monitor, และ track data lineage

- **เหตุผลที่เลือก:** Software-Defined Assets first-class, lineage visualization,
  data engineering focused, Helm deployment บน K8s
- **Deployment:** Helm chart บน Minikube


## Data Warehouse: ClickHouse

Columnar OLAP database สำหรับเก็บ transformed data พร้อม query วิเคราะห์

- **เหตุผลที่เลือก:** Industry standard open-source DWH, columnar storage,
  aggregation query เร็ว, production-grade, K8s ready
- **Deployment:** Helm chart บน Minikube
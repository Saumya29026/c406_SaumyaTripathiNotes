# Comprehensive Error Monitoring Dashboard in Grafana

This guide explains how to create a detailed error monitoring dashboard in Grafana. 
The dashboard will track key performance metrics, detect issues, and help debug errors in a Kubernetes environment using Prometheus as the data source.

---

## Step 1: Access Grafana and Start a New Dashboard

### 1.1 Ensure Port-Forwarding for Grafana

Run the following command to enable port-forwarding:

```bash
kubectl port-forward svc/grafana -n monitoring 3000:80
```

### 1.2 Open Grafana in Your Browser
Navigate to `http://localhost:3000` and log in with:
- **Username:** `****`
- **Password:** `****`

### 1.3 Create a New Dashboard
- Click the **+** icon in the left sidebar
- Select **Dashboard**
- Click **Add visualization**

---

## Step 2: Create a Container Restart Count Panel

### Why?
Container restarts indicate potential application failures.

### Steps:
1. Select "Prometheus" as the data source.
2. Enter the PromQL query:
   ```promql
   sum by(pod) (kube_pod_container_status_restarts_total{namespace="sample-app"})
   ```
3. Choose "Stat" as visualization.
4. Configure thresholds:
   - **0-1:** Green
   - **1-5:** Orange
   - **5+:** Red
5. Click "Apply".

---

## Step 3: Create a Pod Health Status Panel

### Why?
This panel shows non-running pods, helping identify unhealthy pods.

### Steps:
1. Select "Prometheus" as the data source.
2. Use this query:
   ```promql
   sum by(pod) (kube_pod_status_phase{namespace="sample-app", phase!="Running"})
   ```
3. Choose "Table" visualization.
4. Apply color styling for unhealthy pods (Red if `>0`).
5. Click "Apply".

---

## Step 4: Create a Memory Usage Panel

### Why?
High memory usage often leads to performance issues or OOM kills.

### Steps:
1. Select "Prometheus" as the data source.
2. Use this PromQL query:
   ```promql
   sum by(pod) (container_memory_usage_bytes{namespace="sample-app"}) / 
   sum by(pod) (container_spec_memory_limit_bytes{namespace="sample-app"}) * 100
   ```
3. Choose "Gauge" visualization.
4. Configure thresholds:
   - **0-70:** Green
   - **70-85:** Orange
   - **85-100:** Red
5. Click "Apply".

---

## Step 5: Create a CPU Usage Panel

### Why?
High CPU usage can indicate performance bottlenecks.

### Steps:
1. Use this PromQL query:
   ```promql
   sum by(pod) (rate(container_cpu_usage_seconds_total{namespace="sample-app"}[5m])) / 
   sum by(pod) (kube_pod_container_resource_limits_cpu_cores{namespace="sample-app"}) * 100
   ```
2. Choose "Gauge" visualization.
3. Configure thresholds similar to memory usage.
4. Click "Apply".

---

## Step 6: Create an HTTP Error Rate Panel

### Why?
Tracks the percentage of HTTP 5xx errors.

### Steps:
1. Use this PromQL query:
   ```promql
   sum(rate(http_requests_total{namespace="sample-app", status_code=~"5.."}[5m])) / 
   sum(rate(http_requests_total{namespace="sample-app"}[5m])) * 100
   ```
2. Choose "Time series" visualization.
3. Configure thresholds:
   - **0-1%:** Green
   - **1-5%:** Orange
   - **5%+**: Red
4. Click "Apply".

---

## Step 7: Create a Slow Response Panel

### Why?
Monitors API latency using the 95th percentile response time.

### Steps:
1. Use this PromQL query:
   ```promql
   histogram_quantile(0.95, sum by(le) (rate(http_request_duration_seconds_bucket{namespace="sample-app"}[5m])))
   ```
2. Choose "Time series" visualization.
3. Set unit to "Seconds".
4. Click "Apply".

---

## Step 8: Create a Failed Pod Scheduling Panel

### Why?
Shows failed pod scheduling attempts.

### Steps:
1. Use this query:
   ```promql
   sum(kube_pod_status_scheduled{namespace="sample-app", condition="false"})
   ```
2. Choose "Stat" visualization.
3. Configure thresholds:
   - **0:** Green
   - **1+:** Red
4. Click "Apply".

---

## Step 9: Create an OOM (Out of Memory) Kill Counter

### Why?
OOM kills indicate memory exhaustion.

### Steps:
1. Use this query:
   ```promql
   sum(container_oom_events_total{namespace="sample-app"})
   ```
2. Choose "Stat" visualization.
3. Configure thresholds similar to failed pod scheduling.
4. Click "Apply".

---

## Step 10: Arrange Your Dashboard

### Suggested Layout:
1. **Top row:** Container Restarts, Pod Health Issues, OOM Kill Events
2. **Middle row:** Memory Usage, CPU Usage
3. **Bottom row:** HTTP Error Rate, Response Time, Failed Pod Scheduling

### Steps:
1. Resize and arrange panels for better readability.
2. Click "Save" and name it **Comprehensive Error Monitoring**.

---

## Step 11: Configure Dashboard Settings

### General Settings
1. Click the gear icon ⚙️ in the top-right.
2. Add a detailed description.

### Add Variables (For Reusability)
1. Create a variable `namespace`.
2. Query:
   ```promql
   label_values(kube_namespace_labels, namespace)
   ```
3. Enable "Multi-value" and "Include All option".

### Time Settings
1. Enable auto-refresh every **10s**.

---

## Step 12: Verify and Test

1. Check if panels populate data.
2. Trigger a test error to see real-time updates.
3. (Optional) Add alert rules for critical panels.

---

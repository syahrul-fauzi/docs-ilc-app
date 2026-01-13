# 🚀 Deployment Guide (Expo EAS)

## 🛠 Persiapan
1. Pastikan `app.json` memiliki `version` dan `buildNumber` yang benar.
2. Login ke EAS: `eas login`.

## 📦 Build Process
- **Staging**: `eas build --profile staging --platform all`
- **Production**: `eas build --profile production --platform all`

## 📤 Submission
- Kirim ke toko aplikasi: `eas submit --platform ios/android`

## 7. Production Scalability & Performance

To handle the 1000 RPS target in production, the following optimizations have been implemented:

### 7.1 Node.js Clustering
The AI Gateway is configured to use the `cluster` module, distributing the workload across all available CPU cores. This reduces the per-core CPU utilization from ~82% to a more sustainable ~20-30% across multiple workers.
- **Reference**: `scripts/optimizations/gateway-cluster.ts`
- **Benefit**: Improved throughput and high availability.

### 7.2 Optimized Security Guards
The PII protection layer has been refined with:
- **Refined Regex**: Faster patterns for NIK, NPWP, and Phone numbers.
- **Memoization**: Caching layer for frequently matched strings (up to 1000 entries).
- **Parallel Processing**: Simultaneous regex execution for different PII types.
- **Reference**: `scripts/optimizations/optimized-masking.ts`

### 7.3 Kubernetes Horizontal Scaling (HPA)
Automatic scaling based on the 1000 RPS benchmark.
- **Trigger**: 70% CPU Utilization.
- **Min Replicas**: 3.
- **Max Replicas**: 20.
- **Pod Disruption Budget**: Ensures at least 2 pods are available during updates.
- **Manifests**: `infrastructure/k8s/hpa.yaml`, `infrastructure/k8s/pdb.yaml`

## 8. Rollback Procedures
- **AI Gateway**: `kubectl rollout undo deployment/ai-gateway`
- **Scaling**: Revert HPA with `kubectl delete hpa ai-gateway-hpa`
- **Code**: Git revert to stable tag and redeploy via EAS.
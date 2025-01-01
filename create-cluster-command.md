```bash
eksctl create cluster \
—name demo-cluster \
—version 1.31 \
—region us-east-1 \
—nodegroup-name demo-nodes \
—node-type t2.micro \
—nodes 2 \
—nodes-min 1 \
—nodes-max 3
```

kops create cluster \
--name mustafa.k8s.local \
--cloud aws \
--zones us-east-2a,us-east-2b \
--control-plane-count 1 \
--control-plane-size t3.small \
--control-plane-volume-size 30 \
--node-count 2 \
--node-size t3.micro \
--node-volume-size 20 \
--dns private

  export KOPS_STATE_STORE=s3://mustafa-project-kops-state-store-12345
  kops delete cluster --name mustafa.k8s.local --yes

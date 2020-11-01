
up: start-cluster install-platform set-namespace create-secret apply-resource apply-tasks apply-pipelines

install-platform: namespaces install-cicd install-monitoring install-logging

down:
	make down -f ../../k8s-sandbox/Makefile

start-cluster:
	make cluster-up logs repos -f ../../k8s-sandbox/Makefile

namespaces:
	kubectl apply -f ../../k8s-sandbox/platform/namespaces/namespaces.yaml

install-cicd:
	echo "cicd: install" | tee -a output.log
	kubectl apply -f https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
	kubectl apply -f https://storage.googleapis.com/tekton-releases/dashboard/latest/tekton-dashboard-release.yaml
	kubectl patch svc tekton-dashboard -n tekton-pipelines --type='json' -p '[{"op":"replace", "path":"/spec/type", "value":"NodePort"}]'
	kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/git-clone/0.2/git-clone.yaml

install-monitoring: install-prometheus install-grafana

install-prometheus:
	echo "Monitoring: install-grafana" | tee -a output.log
	helm install -n monitoring -f ../../k8s-sandbox/platform/monitoring/prometheus-values.yaml prometheus prometheus-community/prometheus| tee -a output.log

install-grafana:
	echo "Monitoring: install-grafana" | tee -a output.log
	helm install grafana grafana/grafana -n monitoring -f ../../k8s-sandbox/platform/monitoring/grafana-values.yaml | tee -a output.log

install-logging:
	echo "Logging: install-elasticsearch" | tee -a output.log
	helm install elasticsearch elastic/elasticsearch -n logging -f ../../k8s-sandbox/platform/logging/elastic-values.yaml | tee -a output.log
	echo "Logging: install-fluent-bit" | tee -a output.log
	helm install fluent-bit fluent/fluent-bit -n logging -f ../../k8s-sandbox/platform/logging/fluent-values.yaml | tee -a output.log
	echo "Logging: install-kibana" | tee -a output.log
	helm install kibana elastic/kibana -n logging -f ../../k8s-sandbox/platform/logging/kibana-values.yaml | tee -a output.log

create-secret: login docker-secret

login:
	docker login

docker-secret:
	kubectl create secret generic docker-creds -n tekton-pipelines \
 	--from-file=.dockerconfigjson=/home/ubuntu/.docker/config.json \
 	--type=kubernetes.io/dockerconfigjson || true

set-namespace:
	kubectl config set-context --current --namespace=tekton-pipelines

apply-resource:
	kubectl apply -f resource/

apply-tasks:
	kubectl apply -f tasks/

apply-pipelines: carts frontend orders payment queue-master shipping user catalogue

delete-all: delete-tasks delete-pipelines

delete-pipelines: delete-carts delete-catalogue delete-frontend delete-orders delete-payment delete-queue-master delete-shipping delete-user

delete-tasks:
	kubectl delete -f tasks/

ls-test:
	kubectl get all -n test

ls-prod:
	kubectl get all -n production

delete-test:
	kubectl delete all --all -n test
	#kubectl delete ingress socks-ingress -n test || true

delete-prod:
	kubectl delete all --all -n production 
	#kubectl delete ingress socks-ingress -n production || true

catalogue:
	kubectl apply -f ./pipelines/catalogue-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-catalogue-pipeline.yml
delete-catalogue:
	kubectl delete -f ./pipelineRuns/run-catalogue-pipeline.yml || true
	kubectl delete -f ./pipelines/catalogue-pipeline.yml || true

frontend:
	kubectl apply -f ./pipelines/frontend-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-frontend-pipeline.yml

delete-frontend:
	kubectl delete -f ./pipelineRuns/run-frontend-pipeline.yml || true
	kubectl delete -f ./pipelines/frontend-pipeline.yml || true

user:
	kubectl apply -f ./pipelines/user-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-user-pipeline.yml

delete-user:
	kubectl delete -f ./pipelineRuns/run-user-pipeline.yml || true
	kubectl delete -f ./pipelines/user-pipeline.yml || true

orders:
	kubectl apply -f ./pipelines/orders-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-orders-pipeline.yml

delete-orders:
	kubectl delete -f ./pipelineRuns/run-orders-pipeline.yml || true
	kubectl delete -f ./pipelines/orders-pipeline.yml || true

carts:
	kubectl apply -f ./pipelines/carts-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-carts-pipeline.yml

delete-carts:
	kubectl delete ./pipelineRuns/run-carts-pipeline.yml || true
	kubectl delete ./pipelines/carts-pipeline.yml || true

payment:
	kubectl apply -f ./pipelines/payment-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-payment-pipeline.yml

delete-payment:
	kubectl delete -f ./pipelineRuns/run-payment-pipeline.yml || true
	kubectl delete -f ./pipelines/payment-pipeline.yml || true

shipping:
	kubectl apply -f ./pipelines/shipping-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-shipping-pipeline.yml

delete-shipping:
	kubectl delete -f ./pipelineRuns/run-shipping-pipeline.yml || true
	kubectl delete -f ./pipelines/shipping-pipeline.yml || true

queue-master:
	kubectl apply -f ./pipelines/queue-master-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-queue-master-pipeline.yml

delete-queue-master:
	kubectl delete -f ./pipelineRuns/run-queue-master-pipeline.yml || true
	kubectl delete -f ./pipelines/queue-master-pipeline.yml || true


up: create-secret apply-rbac apply-resource apply-tasks apply-pipelines

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

apply-pipelines: carts catalogue frontend orders payment queue-master shipping user

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
	kubectl apply -f ./pipelines/run-catalogue-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-catalogue-pipeline.yml
delete-catalogue:
	kubectl delete -f ./pipelineRuns/run-catalogue-pipeline.yml || true
	kubectl delete -f ./pipelines/run-catalogue-pipeline.yml || true

frontend:
	kubectl apply -f ./pipelines/run-frontend-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-frontend-pipeline.yml

delete-frontend:
	kubectl delete -f ./pipelineRuns/run-frontend-pipeline.yml || true
	kubectl delete -f ./pipelines/run-frontend-pipeline.yml || true

user:
	kubectl apply -f ./pipelines/run-user-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-user-pipeline.yml

delete-user:
	kubectl delete -f ./pipelineRuns/run-user-pipeline.yml || true
	kubectl delete -f ./pipelines/run-user-pipeline.yml || true

orders:
	kubectl apply -f ./pipelines/run-orders-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-orders-pipeline.yml

delete-orders:
	kubectl delete -f ./pipelineRuns/run-orders-pipeline.yml || true
	kubectl delete -f ./pipelines/run-orders-pipeline.yml || true

carts:
	kubectl apply -f ./pipelines/run-carts-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-carts-pipeline.yml

delete-carts:
	kubectl delete ./pipelineRuns/run-carts-pipeline.yml || true
	kubectl delete ./pipelines/run-carts-pipeline.yml || true

payment:
	kubectl apply -f ./pipelines/run-payment-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-payment-pipeline.yml

delete-payment:
	kubectl delete -f ./pipelineRuns/run-payment-pipeline.yml || true
	kubectl delete -f ./pipelines/run-payment-pipeline.yml || true

shipping:
	kubectl apply -f ./pipelines/run-shipping-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-shipping-pipeline.yml

delete-shipping:
	kubectl delete -f ./pipelineRuns/run-shipping-pipeline.yml || true
	kubectl delete -f ./pipelines/run-shipping-pipeline.yml || true

queue-master:
	kubectl apply -f ./pipelines/run-queue-master-pipeline.yml
	kubectl apply -f ./pipelineRuns/run-queue-master-pipeline.yml

delete-queue-master:
	kubectl delete -f ./pipelineRuns/run-queue-master-pipeline.yml || true
	kubectl delete -f ./pipelines/run-queue-master-pipeline.yml || true


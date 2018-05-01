build:
	docker build -t k8sapp/api src/api
	docker build -t k8sapp/nginx src/nginx
	docker build -t k8sapp/db src/db

push:
	docker tag k8sapp/api vlkdev/k8sapp-api && docker push vlkdev/k8sapp-api
	docker tag k8sapp/nginx vlkdev/k8sapp-nginx && docker push vlkdev/k8sapp-nginx
	docker tag k8sapp/db vlkdev/k8sapp-db && docker push vlkdev/k8sapp-db


start-cluster:
	kubectl create -f k8s/database.yml
	kubectl create -f k8s/api.yml
	kubectl create -f k8s/nginx.yml

remove-cluster:
	kubectl delete all --all
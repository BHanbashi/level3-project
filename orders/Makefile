build:
	DOCKER_BUILDKIT=1 docker build --progress=plain -t bhanbashi/orders .

run:
	docker run -it --rm -u 1001:1001 -d --name orders -p 8082:8080 bhanbashi/orders

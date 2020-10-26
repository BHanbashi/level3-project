build:
	DOCKER_BUILDKIT=1 docker build --progress=plain -t bhanbashi/carts .

run:
	docker run -it --rm -u 1001:1001 -d --name carts -p 8083:8080 bhanbashi/carts

build:
	DOCKER_BUILDKIT=1 docker build --progress=plain --tag bhanbashi/shipping .

run:
	docker run -it --rm -u 1001:1001 -d --name shipping -p 8083:8080 bhanbashi/shipping


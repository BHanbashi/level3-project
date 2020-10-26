build:
	DOCKER_BUILDKIT=1 docker build --progress=plain -t bhanbashi/queue-master .

run:
	docker run -it --rm -u 1001:1001 -d --name queue-master -p 8088:8080 bhanbashi/queue-master

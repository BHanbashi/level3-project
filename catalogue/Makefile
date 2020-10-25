NAME = bhanbashi/catalogue
DBNAME = bhanbashi/catalogue-db

TAG=$(TRAVIS_COMMIT)

INSTANCE = catalogue

.PHONY: default copy test

default: test

build:
	docker build -t $(NAME) -f ./docker/catalogue/Dockerfile .
	docker build -t $(DBNAME) -f ./docker/catalogue-db/Dockerfile .
run:
	#docker run -d -t --rm -p 8085:80 $(NAME)
	docker run -d --name $(INSTANCE)db -h $(INSTANCE)db $(DBNAME)
	docker run -d --name $(INSTANCE) -p 8085:80 --link $(INSTANCE)db $(NAME)

test: 
	GROUP=weaveworksdemos COMMIT=test ./scripts/build.sh
	./test/test.sh unit.py
	./test/test.sh container.py --tag $(TAG)

dockertravisbuild: build
	docker build -t $(NAME):$(TAG) -f docker/catalogue/Dockerfile-release docker/catalogue/
	docker build -t $(DBNAME):$(TAG) -f docker/catalogue-db/Dockerfile docker/catalogue-db/
	docker login -u $(DOCKER_USER) -p $(DOCKER_PASS)
	scripts/push.sh

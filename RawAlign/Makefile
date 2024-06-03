ALL: docker-build


# get image tag from git submodule under ./RawAlign 
DOCKER_IMAGE=haliliceylanua/rawalign:$(shell git -C RawAlign describe --tags --always)

git-submodule-init-recursive:
	git submodule update --init --recursive

docker-build: git-submodule-init-recursive
	docker build -t $(DOCKER_IMAGE) .

docker-push:
	docker tag $(DOCKER_IMAGE) haliliceylanua/rawalign:latest
	docker push $(DOCKER_IMAGE)
	docker push haliliceylanua/rawalign:latest
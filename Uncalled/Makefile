ALL: docker-build


# get image tag from git submodule under ./UNCALLED
DOCKER_IMAGE=haliliceylanua/uncalled:$(shell git -C UNCALLED describe --tags --always)

git-submodule-init-recursive:
	git submodule update --init --recursive

docker-build: git-submodule-init-recursive
	docker build -t $(DOCKER_IMAGE) .

docker-push:
	docker tag $(DOCKER_IMAGE) haliliceylanua/uncalled:latest
	docker push $(DOCKER_IMAGE)
	docker push haliliceylanua/uncalled:latest
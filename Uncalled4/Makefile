ALL: docker-build


# get image tag from git submodule under ./uncalled4 
DOCKER_IMAGE=haliliceylanua/uncalled4:$(shell git -C uncalled4 describe --tags --always)

git-submodule-init-recursive:
	git submodule update --init --recursive

docker-build: git-submodule-init-recursive
	docker build -t $(DOCKER_IMAGE) .

docker-push:
	docker tag $(DOCKER_IMAGE) haliliceylanua/uncalled4:latest
	docker push $(DOCKER_IMAGE)
	docker push haliliceylanua/uncalled4:latest
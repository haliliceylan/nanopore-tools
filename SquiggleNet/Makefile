ALL: docker-build

DOCKER_IMAGE=lraes/squigglenet:$(shell git -C SquiggleNet describe --tags --always)-$(shell git log -1 --format=%h .)

git-submodule-init-recursive:
	git submodule update --init --recursive

docker-build: git-submodule-init-recursive
	docker build -t $(DOCKER_IMAGE) .

docker-push:
	docker tag $(DOCKER_IMAGE) lraes/squigglenet:latest
	docker push $(DOCKER_IMAGE)
	docker push lraes/squigglenet:latest

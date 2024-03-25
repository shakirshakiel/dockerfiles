IMAGE_PREFIX := shakirshakiel/awscli-utils
IMAGE_VERSION := 1.0
TRIVY_TARNAME := trivy.tar
.DEFAULT_GOAL := all

docker/build: ## Build docker image
	docker build . -f Dockerfile -t $(IMAGE_PREFIX):$(IMAGE_VERSION)

docker/push: ## Push docker image
	docker push $(IMAGE_PREFIX):$(IMAGE_VERSION)

hadolint: ## Run linting of docker files
	docker run --rm -i -v $(PWD)/hadolint.yaml:/root/.config/hadolint.yaml \
		hadolint/hadolint < ./Dockerfile

docker/save: ## Save docker image to a tar file
	docker save $(IMAGE_PREFIX):$(IMAGE_VERSION) -o $(TRIVY_TARNAME) && chmod 0644 $(TRIVY_TARNAME)

trivy: docker/save ## Run trivy to detect vulnerabilities
	@docker run -v $(PWD):/workdir \
		-v $(PWD)/.trivycache:/var/lib/trivy \
		-w /workdir \
		aquasec/trivy --exit-code 1 --exit-on-eol 1 \
		--severity CRITICAL \
		--cache-dir /var/lib/trivy image --ignore-unfixed \
		--scanners vuln --scanners secret --scanners license --scanners config --image-config-scanners config \
		--input /workdir/$(TRIVY_TARNAME)

all: docker/build hadolint trivy docker/push
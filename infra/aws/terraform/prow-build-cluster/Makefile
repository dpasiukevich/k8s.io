# Copyright 2023 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

TF ?= terraform
TF_ARGS ?=

# TODO: figure out a workaround for: https://github.com/hashicorp/terraform-provider-kubernetes-alpha/issues/199#issuecomment-832614387
DEPLOY_K8S_RESOURCES ?= true

# Valid values are: canary, prod
PROW_ENV ?= canary

.PHONY: init
init:
	$(TF) $@ \
		-backend-config=./tfbackends/$(PROW_ENV).tfbackend

.PHONY: plan
plan:
	$(TF) $@ $(TF_ARGS) \
		-var-file=./terraform.tfvars \
		-var-file=./terraform.$(PROW_ENV).tfvars \
		-var="deploy_kubernetes_resources=$(DEPLOY_K8S_RESOURCES)"

.PHONY: apply
apply:
	$(TF) $@ $(TF_ARGS) \
		-var-file=./terraform.tfvars \
		-var-file=./terraform.$(PROW_ENV).tfvars \
		-var="deploy_kubernetes_resources=$(DEPLOY_K8S_RESOURCES)"

.PHONY: destroy
destroy:
	$(TF) $@ $(TF_ARGS) \
		-var-file=./terraform.tfvars \
		-var-file=./terraform.$(PROW_ENV).tfvars \
		-var="deploy_kubernetes_resources=$(DEPLOY_K8S_RESOURCES)"

.PHONY: fmt
fmt:
	$(TF) $@

.PHONY: output
output:
	$(TF) $@

.PHONY: clean
clean:
	rm -rf ./.terraform

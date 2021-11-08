build: clean ../main.yaml

../main.yaml: main.yaml
	kustomize build >$@

main.yaml: clean/main.yaml
	kustomize build clean >$@

clean/main.yaml: clean/values.yaml
	-helm repo add kong https://charts.konghq.com
	helm repo update
	helm template kong kong/kong \
		--version 2.5.0 --namespace=kong --values=clean/values.yaml --include-crds --kube-version 1.21 >$@

.PHONY: clean
clean:
	rm -f ../main.yaml main.yaml clean/main.yaml

# GKE GRPC examples

## External Ingress example

### Apply the configuration to your cluster
* Creae and configure an SSL certififcate to be used in the ingress.  The cerficate referenced using the name `test` in the `ingress-example.yaml`.
```
openssl genrsa -out test-ingress.key 2048
openssl req -new -key test-ingress.key -out test-ingress.csr \
    -subj "/CN=test.com"
openssl x509 -req -days 365 -in test-ingress.csr -signkey test-ingress.key \
    -out test-ingress.crt
gcloud compute ssl-certificates create test \
    --certificate=test-ingress.crt \
    --private-key=test-ingress.key
```
* Apply the kubernetes configuration
```
kubectl apply -f ingress-example.yaml
```

### Test the GRPC service 
* Set the variable `IP` to the loadbalancers external ip.
```
grpcurl -insecure -d '{"greeting":"tester"}' $IP:443 hello.HelloService/SayHello
```


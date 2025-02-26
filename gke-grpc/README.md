# GKE GRPC examples

## External Ingress example

## Apply the configuration to your cluster
```
kubectl apply -f ingress-example.yaml
```
## Test the GRPC service 
* Set the variable `IP` to the loadbalancers external ip.
```
grpcurl -insecure -d '{"greeting":"tester"}' $IP:443 hello.HelloService/SayHello
```


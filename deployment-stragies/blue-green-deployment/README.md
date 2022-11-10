$ kubectl patch service my-app-svc -p '{"spec":{"selector":{"version":"v2.0.0"}'
# kubectl delete deploy my-app1

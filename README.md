# SIMULAZIONE

## Passaggi:

1. Dopo aver installato **kubectl** ed averlo avviato:
   ```bash
   kubectl start
   ```

2. Avvio della dashboard di Minikube:
   ```bash
   minikube dashboard
   ```
   In questo modo, nella sezione **Pods** troverai tutte le immagini scaricate.

3. Scarico il classico **HelloMinikube** (deprecato):
   ```bash
   kubectl run hello-minikube-2 --image=kicbase/echo-server:1.0 --port=8080
   ```

4. Ora si usa:
   ```bash
   kubectl create deployment hello-minikube-test --image=registry.k8s.io/e2e-test-images/agnhost:2.39 --port=8080
   ```

5. Esporre il servizio all'esterno (renderlo accessibile fuori dal cluster):
   ```bash
   kubectl expose deployment hello-minikube-test --type=NodePort
   ```

6. Ottenere l'URL del servizio esposto:
   ```bash
   minikube service hello-minikube-test --url
   ```

## ALCUNI COMANDI UTILI:

- Visualizzare i servizi:
  ```bash
  kubectl get services
  ```

- Verificare il deployment:
  ```bash
  kubectl get deployment hello-minikube-test
  ```

- Controllare i log di Minikube:
  ```bash
  minikube logs
  ```

## Lezione 1 - Come fare un proprio deployment di Tomcat da eseguire fuori
### in esempio 1 è presente il file da scaricare o creare
1. Applicare il file di deployment:
   ```bash
   kubectl apply -f ./deployment.yaml
   ```

2. Esporre il deployment di Tomcat:
   ```bash
   kubectl expose deployment tomcat-deployment --type=NodePort
   ```
3. Esporre il deployment di Tomcat, che naturalmente dovrà essere bilanciato:
   ```bash
    kubectl scale --replicas=4 deployment/tomcat-deployment
   kubectl expose deployment tomcat-deployment --type=LoadBalancer --port=8080 --target-port=8080 --name=tomcat-load-balancerservice/tomcat-load-balancer exposed
   ```
3. Comandi utili al deploy (rollout e update)
   ```bash
   kubectl rollout status
   kubectl set image
   kubectl rollout history
   ```

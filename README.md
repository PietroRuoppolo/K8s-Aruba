# ☸️ Kubernetes Ticketing App – Aruba Cloud Deployment

## 📖 Descrizione

Questo progetto mostra come distribuire un’applicazione di **ticketing** su un cluster **Aruba Managed Kubernetes**, rendendola accessibile dall’esterno tramite **NGINX Ingress Controller** e un **Service LoadBalancer**.  
Il sistema integra un database **MongoDB** con storage persistente.


---

## 🎯 Obiettivi del progetto

- ☸️ Utilizzare Kubernetes per orchestrare applicazione e database  
- 🧱 Configurare networking cloud su Aruba (VPC, subnet, Load Balancer)  
- 🔐 Gestire sicurezza tramite ServiceAccount, RBAC e Secret  
- 📦 Implementare persistenza dati con PVC e MongoDB  
- 🌐 Esporre l’app pubblicamente tramite Ingress Controller  
- 💪 Garantire resilienza con distribuzione multi-AZ  

---

## 🧠 Architettura del progetto

L’architettura è composta da tre livelli principali:

### 📡 Livello Networking & Ingress
- **Service LoadBalancer** → punto di ingresso pubblico  
- **NGINX Ingress Controller** → instrada il traffico verso i servizi interni  
- **IngressClass (default)** → assegna il controller come gestore di tutte le risorse Ingress  
- **Ingress Rules** → routing verso l’app ticketing  

### 📦 Livello Applicazione
- Deployment dell’app **ticketing**
- ReplicaSet con **topologySpreadConstraints** per distribuire i Pod su più AZ
- Service interno `ClusterIP`
- Configurazioni tramite Secret e ConfigMap
- RBAC minimali per sicurezza

### 🗄️ Livello Database
- Deployment **MongoDB**
- PVC per storage persistente (WaitForFirstConsumer)
- Service interno `mongo-service` per accesso dai microservizi

---
## 🌐 Endpoint principali dell’app

| Metodo | Endpoint | Descrizione |
|-------|----------|-------------|
| `GET` | `/health` | Stato dell'app |
| `GET` | `/tickets` | Recupera i ticket |
| `POST` | `/tickets` | Crea un nuovo ticket |
| `GET` | `/` | Pagina principale |

*(Gli endpoint possono variare in base all’applicazione effettiva.)*

---
---

## 🚀 Deployment del progetto

Assicurati che:
- il tuo kubeconfig Aruba sia configurato  
- `kubectl` sia operativo  
- il cluster abbia nodi su più AZ  

🔍 Verifica dello stato del cluster
kubectl get pods -A
kubectl get svc -A
kubectl get ingress -A
kubectl get pvc -A

Quando il Service di tipo LoadBalancer del controller ottiene un EXTERNAL-IP, l’app diventa raggiungibile dall’esterno.

🧹 Pulizia completa
kubectl delete namespace ticketing-app
kubectl delete pvc --all -A
kubectl delete pv --all

Poi eliminare:
	•	Load Balancer
	•	Cluster Kubernetes
	•	VPC e subnet su Aruba

📘 Conclusione

Questo progetto rappresenta un esempio completo di deployment su cloud reale, mostrando come:
	•	costruire un ambiente Kubernetes robusto
	•	integrare servizi applicativi e database
	•	configurare ingressi e routing HTTP avanzati
	•	utilizzare pattern di resilienza multi-AZ

È un’ottima base per ruoli come Cloud Engineer, DevOps, Kubernetes Specialist oppure come progetto portfolio su GitHub.



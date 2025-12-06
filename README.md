# ☸️ Kubernetes Ticketing App – Aruba Cloud Deployment

## 📖 Descrizione

Questo progetto mostra come distribuire un’applicazione di **ticketing** su un cluster **Aruba Managed Kubernetes**, rendendola accessibile dall’esterno tramite **NGINX Ingress Controller** e un **Service LoadBalancer**.  
Il sistema integra un database **MongoDB** con storage persistente, configurato tramite **Persistent Volume Claim** e provisioning dinamico.

Il progetto dimostra competenze nella progettazione e gestione di infrastrutture Kubernetes reali: networking, sicurezza, ingressi, deployment multi-AZ e integrazione tra applicazione e database.

---

## 🎯 Obiettivi del progetto

- ☸️ Utilizzare Kubernetes per orchestrare applicazione e database  
- 🧱 Configurare networking cloud su Aruba (VPC, subnet, Load Balancer)  
- 🔐 Gestire sicurezza tramite ServiceAccount, RBAC e Secret  
- 📦 Implementare persistenza dati con PVC e MongoDB  
- 🌐 Esporre l’app pubblicamente tramite Ingress Controller  
- 💪 Garantire resilienza con distribuzione multi-AZ  
- 🧩 Dimostrare architettura a microservizi in ambiente Kubernetes  

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

## 📂 Struttura del repository

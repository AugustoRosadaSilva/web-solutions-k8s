# Web Solutions - Docker e Kubernetes

## 1. Descrição do Projeto

Este projeto apresenta uma prova de conceito de modernização da infraestrutura da empresa Web Solutions Ltda., utilizando tecnologias de conteinerização e orquestração.

A solução implementa dois servidores web independentes:

- Nginx
- Apache HTTPD

Ambos executados em containers Docker e gerenciados por um cluster Kubernetes.

---

# 2. Objetivo

O objetivo é demonstrar como a utilização de Docker e Kubernetes pode melhorar:

- Escalabilidade das aplicações;
- Padronização dos ambientes;
- Facilidade de implantação;
- Gerenciamento dos serviços;
- Independência entre aplicações.

---

# 3. Tecnologias Utilizadas

- Docker
- Docker Desktop
- Kubernetes
- Minikube
- kubectl
- YAML
- Visual Studio Code

---

# 4. Arquitetura da Solução

A arquitetura desenvolvida possui:

```
Usuário
   |
   |
Kubernetes Cluster
   |
   |----------------|
   |                |
Nginx Deployment   Apache Deployment
   |                |
Pods               Pods
   |                |
Nginx Container    Apache Container
```

---

# 5. Estrutura do Projeto

```
web-solutions-k8s/

├── nginx/
│   ├── Dockerfile
│   └── index.html
│
├── apache/
│   ├── Dockerfile
│   └── index.html
│
├── kubernetes/
│   ├── nginx-deployment.yaml
│   ├── nginx-service.yaml
│   ├── apache-deployment.yaml
│   └── apache-service.yaml
│
└── README.md
```

---

# 6. Criação das Imagens Docker

## Nginx

Construção da imagem:

```
docker build -t nginx-web ./nginx
```

Execução local:

```
docker run -d -p 8080:80 nginx-web
```

---

## Apache HTTPD

Construção da imagem:

```
docker build -t apache-web ./apache
```

Execução local:

```
docker run -d -p 8081:80 apache-web
```

---

# 7. Configuração Kubernetes

As imagens foram carregadas no Minikube:

```
minikube image load nginx-web

minikube image load apache-web
```

---

# 8. Implantação no Kubernetes

Aplicação dos manifestos:

```
kubectl apply -f kubernetes/
```

---

# 9. Verificação dos Pods

Comando utilizado:

```
kubectl get pods
```

Resultado esperado:

- 2 Pods Nginx funcionando;
- 2 Pods Apache funcionando.

---

# 10. Serviços Kubernetes

Serviços criados:

## Nginx

Service:

```
nginx-service
```

Porta:

```
30080
```

---

## Apache

Service:

```
apache-service
```

Porta:

```
30081
```

---

# 11. Acesso aos Serviços

Nginx:

```
minikube service nginx-service
```

Apache:

```
minikube service apache-service
```

---

# 12. Escalabilidade

O Kubernetes permite aumentar ou reduzir a quantidade de containers.

Exemplo:

Aumentar Nginx para 5 réplicas:

```
kubectl scale deployment nginx-deployment --replicas=5
```

Aumentar Apache para 5 réplicas:

```
kubectl scale deployment apache-deployment --replicas=5
```

---

# 13. Benefícios da Solução

A arquitetura proposta permite:

- Maior disponibilidade;
- Melhor utilização de recursos;
- Facilidade de manutenção;
- Implantações mais rápidas;
- Possibilidade de expansão para novas aplicações.

---

# 14. Conclusão

A implementação demonstrou que Docker e Kubernetes são ferramentas eficientes para modernização da infraestrutura da Web Solutions Ltda.

A utilização de containers possibilita ambientes padronizados e independentes, enquanto o Kubernetes oferece recursos de gerenciamento, escalabilidade e disponibilidade dos serviços.

A solução criada serve como base para futuras migrações de aplicações da empresa para uma arquitetura moderna baseada em nuvem.
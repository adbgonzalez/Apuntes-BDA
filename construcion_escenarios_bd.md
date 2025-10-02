# Construción de solucións propias de Enxeñería de datos

A principal alternativa a empregar solucións **End-to-End comerciais** (como Databricks, Snowflake ou BigQuery) é construír unha solución **personalizada** empregando ferramentas libres en servidores propios (on-premise ou en cloud privada).  

Este enfoque require máis coñecemento técnico e mantemento, pero ofrece **maior control, flexibilidade e independencia de provedores**.  

Para iso é importante coñecer as seguintes tecnoloxías base:

---

## Docker
- **Que é**: Plataforma para crear, distribuír e executar aplicacións illadas en contedores.  
- **Usos en enxeñaría de datos**:
  - Despregue reproducible de servizos como Spark, Kafka, MinIO, Superset, etc.
  - Creación de imaxes personalizadas con dependencias específicas (por exemplo, Python + librarías de ciencia de datos).
  - Execución de contornos de desenvolvemento idénticos para todos os membros do equipo.  
- **Vantaxes**:
  - Lixeiro e rápido comparado con máquinas virtuais.
  - Permite escalar facilmente engadindo máis contedores.  
- **Exemplo**:
  ```bash
  docker run -it --rm apache/spark-py pyspark
  ```
  Executa un contedor de Spark interactivo.

---

## Kubernetes
- **Que é**: Orquestrador de contedores que automatiza o despregue, escalado e xestión de aplicacións distribuídas.  
- **Usos en enxeñaría de datos**:
  - Despregue de clusters de **Spark**, **Kafka** ou **Airflow** en modo altamente dispoñible.
  - Balanceo de carga e recuperación automática de servizos en caso de fallo.
  - Escalado horizontal de procesos de datos en función da demanda.  
- **Vantaxes**:
  - Estándar de facto na orquestración de contedores.
  - Portable: pode executarse en servidores propios ou en calquera nube.  
- **Exemplo**:
  ```bash
  kubectl apply -f spark-cluster.yaml
  ```
  Desprega un cluster de Spark definido nun ficheiro YAML.

---

## Git / GitHub
- **Que é**:  
  - **Git** é un sistema de control de versións distribuído.  
  - **GitHub** (ou GitLab, Bitbucket) son plataformas colaborativas baseadas en Git.  
- **Usos en enxeñaría de datos**:
  - Versionado de código, scripts ETL, configuracións de Docker/Kubernetes e notebooks.
  - Colaboración entre equipos con ramas, revisións (*pull requests*) e integración continua.
  - Documentación de proxectos e pipelines mediante *wikis* ou README.  
- **Vantaxes**:
  - Transparencia no desenvolvemento (quen fixo que cambios e cando).
  - Integración con CI/CD para despregar automaticamente contedores ou pipelines.  
- **Exemplo**:
  ```bash
  git init
  git add .
  git commit -m "Primeiro commit"
  git remote add origin https://github.com/usuario/proxecto.git
  git push -u origin main
  ```

---

## Outras tecnoloxías complementarias
Aínda que Docker, Kubernetes e Git/GitHub son a **base mínima**, unha solución personalizada adoita requirir tamén:

- **Infraestrutura como código (IaC)**:  
  - Terraform, Ansible → para automatizar a creación de servidores e clusters.  
- **Monitorización e logs**:  
  - Prometheus, Grafana, ELK Stack → para controlar rendemento e detectar incidencias.  
- **Bases de datos e almacenamento**:  
  - PostgreSQL, MinIO, HDFS, Cassandra, MongoDB.  
- **Orquestración e pipelines**:  
  - Apache Airflow, Dagster ou Prefect para planificar fluxos de datos.  
- **Seguridade**:  
  - Xestión de credenciais con Vault, autenticación con Keycloak, certificados TLS.  

---

## Vantaxes dunha solución personalizada
- Control total sobre a infraestrutura e datos.  
- Adaptación ao orzamento (uso de hardware propio ou nube híbrida).  
- Flexibilidade para escoller só as ferramentas necesarias.  
- Posibilidade de optimizar custos a longo prazo fronte a licenzas comerciais.  

## Retos e desafíos
- Maior complexidade de mantemento e administración.  
- Necesidade de perfís técnicos especializados (DevOps, Data Engineers).  
- Escalabilidade máis difícil se non se planifica correctamente.  
- Custos ocultos en seguridade, monitorización e soporte.  

# CI/CD Pipeline - cicd-demo

## Flujo del Pipeline
1. **Checkout** - Clona el repositorio desde GitHub
2. **Build & Test** - Compila con Maven (mvn clean package)
3. **Static Analysis** - Análisis de código con SonarQube
4. **Docker Build** - Construye imagen Docker de la aplicación
5. **Container Security Scan** - Escaneo de vulnerabilidades con Trivy
6. **Deploy** - Despliega el contenedor en puerto 9090

## Infraestructura
- Jenkins (contenedor Docker)
- SonarQube 9.9 Community (contenedor Docker)
- Trivy (instalado en el agente Jenkins)

## Gatekeeping
- SonarQube valida calidad y security hotspots
- Trivy bloquea el deploy si detecta vulnerabilidades CRITICAL (--exit-code 1)

## Ejecución
docker compose up -d
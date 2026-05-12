# Unit V: Continuous Integration with GitHub Actions

## 📋 1. Understanding Workflow Automation

Continuous Integration (CI) automates the process of merging code changes into a central repository, where automated builds and tests are run. **GitHub Actions** provides native workflow automation built directly into your GitHub repository.

### Workflow Directory Structure
Workflows are defined by YAML files placed inside the `.github/workflows/` directory at the root of the project.
```text
my-project/
└── .github/
    └── workflows/
        └── ci.yml
```

---

## 🛠️ 2. Core Components of GitHub Actions

- **Workflows:** Configurable automated processes that run one or more jobs.
- **Events:** Specific activities that trigger workflows (e.g., `push`, `pull_request`, `schedule`, `workflow_dispatch`).
- **Jobs:** Set of steps that execute on the same runner. Jobs can run in parallel or sequentially.
- **Steps:** Individual tasks within a job. A step can run shell commands or execute an action.
- **Actions:** Pre-packaged executable units available on the GitHub Marketplace.
- **Runners:** Compute infrastructure that executes jobs. Can be **GitHub-hosted** or **Self-hosted**.

---

## 💻 3. Advanced Workflow & Matrix Strategies

Matrix strategies allow you to test your code across multiple operating systems, languages, or software versions simultaneously within a single job configuration.

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16.x, 18.x, 20.x]
```

---

## 📝 4. End-to-End Workflow Demonstration

Create the file `.github/workflows/ci.yml` at the root of your project:

```yaml
name: CI/CD Multi-Job Integration

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build_and_test:
    name: Build & Run Tests
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code from Repo
      uses: actions/checkout@v4

    - name: Set up JDK 17
      uses: actions/setup-java@v4
      with:
        java-version: '17'
        distribution: 'temurin'
        cache: maven

    - name: Run Maven Tests
      run: mvn test

    - name: Package Maven Artifact
      run: mvn package -DskipTests

  build_docker_image:
    name: Build and Push Docker Image to Docker Hub
    needs: build_and_test
    runs-on: ubuntu-latest
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'

    steps:
    - name: Checkout Code
      uses: actions/checkout@v4

    - name: Log in to Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Build and Push Docker Image
      uses: docker/build-push-action@v5
      with:
        context: .
        push: true
        tags: amit/my-app:latest
```

### GitHub Actions Demonstration (Amit Example)
![Amit terminal running github actions or web ui](./amit_github_actions.png)

## 📸 Complete Unit 5 Visual Gallery (8 Images Total)

````carousel
![GitHub Actions Workflow Directory Topology](./amit_u5_p1.png)
<!-- slide -->
![Jobs Matrix Strategy Execution](./amit_u5_p2.png)
<!-- slide -->
![GitHub Marketplace Actions List](./amit_u5_p3.png)
<!-- slide -->
![GitHub-Hosted Runners Overview](./amit_u5_p4.png)
<!-- slide -->
![Docker Image Build & Push Job Details](./amit_u5_p5.png)
<!-- slide -->
![Caching Mechanism Workflow Configuration](./amit_u5_p6.png)
<!-- slide -->
![End-to-End Multi-Job CI Build Pipeline](./amit_u5_p7.png)
````



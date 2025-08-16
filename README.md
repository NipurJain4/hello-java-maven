# Jenkins + Maven + Java HelloWorld Project

A simple demonstration of setting up a Jenkins CI/CD pipeline for a Java Maven project.

## 🛠️ Tools Required (All Free)

- **Jenkins** (installed locally or via Docker)
- **Java JDK 8 or 11**
- **Maven**
- **Git** (optional — can run from local folder)

## 📂 Project Structure

```
hello-java-maven/
├── src/
│   └── main/
│       └── java/
│           └── HelloWorld.java
├── pom.xml
└── README.md
```
## 🚀 Quick Start

### Step 1: Create the Java Application

Create the directory structure:
```bash
mkdir -p hello-java-maven/src/main/java
cd hello-java-maven
```

Create `src/main/java/HelloWorld.java`:
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Jenkins + Maven!");
    }
}
```

### Step 2: Create Maven Configuration

Create `pom.xml`:
```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>hello</artifactId>
    <version>1.0</version>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

### Step 3: Test Locally 

```bash
# Compile and package
mvn clean package

# Run the application
java -cp target/classes HelloWorld
```

Expected output: `Hello, Jenkins + Maven!`

##  Jenkins Setup
Local Installation

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install jenkins

# Start Jenkins service
sudo systemctl start jenkins
sudo systemctl enable jenkins

# Access Jenkins at http://localhost:8080
```

## ⚙️ Jenkins Configuration

### 1. Configure Maven in Jenkins

1. Go to **Manage Jenkins** → **Global Tool Configuration**
2. Scroll to **Maven** section
3. Click **Add Maven**
4. Name: `Maven-3.8.6` (preferred version)
5. Check **Install automatically**
6. Choose version from dropdown
7. Click **Save**

### 2. Create Jenkins Job

1. Click **New Item**
2. Enter name: `hello-java-maven`
3. Select **Freestyle project**
4. Click **OK**

### 3. Configure the Job

**Source Code Management:**
- Select **Git** (if using repository)
- Repository URL: `https://github.com/YourUsername/hello-java-maven.git`
- Or select **None** if building from local workspace

**Build Steps:**
1. Click **Add build step**
2. Select **Invoke top-level Maven targets**
3. Maven Version: Select the Maven version you configured
4. Goals: `clean package`

**Post-build Actions (Optional):**
- Archive artifacts: `target/*.jar`

### 4. Save and Build

1. Click **Save**
2. Click **Build Now**
3. Check **Console Output** for build results

## ✅ Expected Build Output

```
Started by user admin
Running as SYSTEM
Building in workspace /var/jenkins_home/workspace/hello-java-maven
[hello-java-maven] $ mvn clean package
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------< com.example:hello >-------------------------
[INFO] Building hello 1.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ hello ---
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ hello ---
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ hello ---
[INFO] Compiling 1 source file to /var/jenkins_home/workspace/hello-java-maven/target/classes
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ hello ---
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ hello ---
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ hello ---
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ hello ---
[INFO] Building jar: /var/jenkins_home/workspace/hello-java-maven/target/hello-1.0.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.345 s
[INFO] Final Memory: 15M/56M
[INFO] ------------------------------------------------------------------------
Finished: SUCCESS
```

## 🔧 Troubleshooting

### Common Issues

**1. Git Connection Failed**
```bash
# Check git configuration
git config --list

# Test repository access
git ls-remote -h https://github.com/YourUsername/hello-java-maven.git HEAD
```

**2. Maven Not Found**
- Ensure Maven is configured in Global Tool Configuration
- Check Maven installation path: `/usr/bin/mvn`

**3. Java Compilation Errors**
- Verify Java version compatibility in pom.xml
- Check JAVA_HOME environment variable

**4. Permission Issues**
```bash
# Fix Jenkins user permissions
sudo chown -R jenkins:jenkins /var/lib/jenkins
```

## 📸 Screenshots

### Successful Build Console Output
![Build Success](screenshots/ss1.png)

### Jenkins Job Configuration
![Job Config](screenshots/ss2.png)


1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

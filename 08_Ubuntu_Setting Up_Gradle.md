## Steps to Install Gradle Manually on Linux

### 1. Install Prerequisites

Gradle requires Java (JDK 8 or later). First, check if Java is installed:

```bash
java -version
```

If not installed, install OpenJDK:

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

Verify Java is installed:

```bash
java -version
```

---

### 2. Download the Latest Gradle Release

Visit the Gradle releases page and download it:  
👉 https://gradle.org/releases/

---

### 3. Extract and Move to `/opt/gradle`

```bash
sudo unzip -d /opt/gradle /tmp/gradle-8.13-bin.zip
```

You’ll now have Gradle under `/opt/gradle/gradle-8.13`.

---

### 4. Set Up Environment Variables

Edit your shell config file (`~/.bashrc`, `~/.zshrc`, etc.):

```bash
nano ~/.bashrc
```

Add the following lines at the end:

```bash
export GRADLE_HOME=/opt/gradle/gradle-8.13
export PATH=$GRADLE_HOME/bin:$PATH
```

Save and reload the config:

```bash
source ~/.bashrc
```

---

### 5. Verify Installation

```bash
gradle -v
```

You should see Gradle’s version and environment info.

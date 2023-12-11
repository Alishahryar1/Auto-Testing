```markdown
# AutoTestFramework - Functional

AutoTestFramework - Functional is a Java-based, customizable automated testing framework designed for functional testing of web services (including network traffic) and API services. It seamlessly integrates with AWS services and various databases. The framework supports configuration through key-value pairs in a `config.properties` file located in the resources folder. It also features a secure system for encrypting secrets in the `config.properties` file, which are decrypted at runtime. Detailed setup instructions for encryption and decryption are provided below.

**Framework Technologies:**

* Java
* Maven
* TestNG
* Selenium
* BrowserMob
* MongoDB
* AWS Java SDK

## Setup Instructions

1. **Java JDK Installation**: Download and install the Java JDK.

2. **Maven Configuration**: 
   - Download and configure Maven from [here](https://maven.apache.org/download.cgi?Preferred=ftp://mirror.reverse.net/pub/apache/).

### Generating a Keystore File

Execute the following command to generate a keystore file:
```
keytool -genseckey -keystore .keystore -storetype jceks -storepass "{store_pass}" -keyalg AES -keysize 256 -alias configPasswords -keypass "{key_pass}"
```

### Encryption & Decryption Keys

- Place the `.keystore` file in the user root directory.
- Create a `.vault` file with the following structure and store it in the user root:

  ```
  STORE_PASSWORD=
  KEY_PASSWORD=
  ```

- Fill in `STORE_PASSWORD` and `KEY_PASSWORD` with the values used when generating the keystore file.

## Configuration

- Configure the test groups and environment in the `src/test/resources/testng.xml` file.

### Utilizing AWS Services

- Create a `credentials` file with the following structure and store it in `~/.aws/credentials`:

  ```
  [default]
  aws_access_key_id=
  aws_secret_access_key=

  [devprofile]
  aws_access_key_id=
  aws_secret_access_key=

  [qaprofile]
  aws_access_key_id=
  aws_secret_access_key=
  ```

- Enter your AWS `access key id` and `secret access key` for the specified environments.

## Running Tests From Command Line

- Default parameters:
  ```
  mvn clean test -Denv={environment} -Dgroups={scope}
  ```

- Pointing to a local Selenium server:
  ```
  mvn clean test -Denv={environment} -Dgroups={scope} -Dselenium.grid={seleniumGrid_url}
  ```

- Pointing to a local application instance:
  ```
  mvn clean test -Denv=LOCAL -Dgroups={scope} -Dapphost={local_app_url}
  ```

### Installing a Local Selenium Grid

- Set up a local Selenium grid by installing either a [Selenium server](https://www.seleniumhq.org/docs/07_selenium_grid.jsp) or [Zalenium](https://github.com/zalando/zalenium).

## Viewing Detailed Results

Access detailed test reports at `target/surefire-reports/emailable-report.html`.
```

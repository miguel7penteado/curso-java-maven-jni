# native-maven-plugin-example

Um simples exemplo usando a biblioteca [Native Maven Plugin](https://www.mojohaus.org/maven-native/native-maven-plugin/) 
para construir e distribuir bibliotecas estáticas C++ 
(incluindo arquivos cabeçalho) para um repositório maven 
e então poder compilar e distribuir executáveis C++ 
(tendo dependências apontando para bibliotecas estáticas).

O projeto fornece 3 arquivos pom principais primários.
- Um pom primário para a configuração genérica do Native Maven Plugin.
- Um pom primário para a configuração específica para compilar bibliotecas estáticas.
- Um pom primário para a configuração específica para compilar executáveis.

Adicionalmente, 2 arquétipos do maven são fornecidos:
- com.acme.archetype.cpp:staticLibrary:0.0.1 para rapidamente criar projetos para bibliotecas estáticas
- com.acme.archetype.cpp:executable:0.0.1 to para rapidamente criar projetos para executáveis

## estrutura dos diretórios contendo os `pom.xml`

```bash
.
├── br.com.miguelpenteado.execucao.estatica
│   └── pom.xml
├── br.com.miguelpenteado.execucao.executavel
│   └── pom.xml
├── br.com.miguelpenteado.execucao.principal
│   └── pom.xml
├── br.com.miguelpenteado.projeto.estatica
│   ├── pom.xml
│   └── src
│       ├── main
│       │   └── resources
│       │       ├── archetype-resources
│       │       │   ├── pom.xml
│       │       │   └── src
│       │       │       └── main
│       │       │           └── cpp
│       │       │               ├── __artifactId__
│       │       │               └── header
│       │       └── META-INF
│       │           └── maven
│       └── test
│           └── resources
│               └── projects
│                   └── basic
└── br.com.miguelpenteado.projeto.executavel
    ├── pom.xml
    └── src
        ├── main
        │   └── resources
        │       ├── archetype-resources
        │       │   ├── pom.xml
        │       │   └── src
        │       │       └── main
        │       │           └── cpp
        │       │               └── __artifactId__
        │       └── META-INF
        │           └── maven
        └── test
            └── resources
                └── projects
                    └── basic

```

## Pré-Requisitos para instalar no Sistema Operacional

Existem uns erros bem chatos que aparecem por falta de instalação de 
bibliotecas java compiladas para funcionar com esta versão do Maven ao
que me parece.
Eu opto por instalar tudo que vem com a distribuição para evitar essas
coisas.

### Windows

### Linux

Instale as dependências do maven 3. Eu estou utilizando o debian\devuan
portanto vou instalar todos os pacotes via **apt-get** :

```bash
sudo apt-get install antlr3-gunit-maven-plugin antlr3-maven-plugin \
antlr3.2-gunit-maven-plugin antlr3.2-maven-plugin antlr4-maven-plugin \
jruby-maven-plugins libangular-maven-plugin-java \
libantlr-maven-plugin-java libaspectj-maven-plugin-java \
libavro-maven-plugin-java libbuild-helper-maven-plugin-java \
libclojure-maven-plugin-java libexec-maven-plugin-java \
libgettext-maven-plugin-java libgmavenplus-java \
libhawtjni-maven-plugin-java libjarjar-maven-plugin-java \
libjavacc-maven-plugin-java libmaven-antrun-extended-plugin-java \
libmaven-antrun-plugin-java libmaven-archiver-java \
libmaven-archiver-java-doc libmaven-artifact-transfer-java \
libmaven-assembly-plugin-java libmaven-bundle-plugin-java \
libmaven-clean-plugin-java libmaven-common-artifact-filters-java \
libmaven-common-artifact-filters-java-doc \
libmaven-compiler-plugin-java libmaven-dependency-analyzer-java \
libmaven-dependency-plugin-java libmaven-dependency-tree-java \
libmaven-dependency-tree-java-doc libmaven-deploy-plugin-java \
libmaven-doxia-tools-java libmaven-doxia-tools-java-doc \
libmaven-ejb-plugin-java libmaven-enforcer-plugin-java \
libmaven-exec-plugin-java libmaven-file-management-java \
libmaven-file-management-java-doc libmaven-filtering-java \
libmaven-install-plugin-java libmaven-invoker-java \
libmaven-invoker-plugin-java libmaven-jar-plugin-java \
libmaven-javadoc-plugin-java libmaven-jaxb2-plugin-java \
libmaven-mapping-java libmaven-parent-java \
libmaven-plugin-testing-java libmaven-plugin-tools-java \
libmaven-processor-plugin-java libmaven-reporting-api-java \
libmaven-reporting-exec-java libmaven-reporting-impl-java \
libmaven-reporting-impl-java-doc libmaven-repository-builder-java \
libmaven-repository-builder-java-doc libmaven-resolver-java \
libmaven-resolver-transport-http-java libmaven-resources-plugin-java \
libmaven-scm-java libmaven-scm-java-doc libmaven-scm-providers-java \
libmaven-script-interpreter-java libmaven-shade-plugin-java \
libmaven-shared-incremental-java libmaven-shared-incremental-java-doc \
libmaven-shared-io-java libmaven-shared-io-java-doc \
libmaven-shared-jar-java libmaven-shared-jar-java-doc \
libmaven-shared-utils-java libmaven-shared-utils-java-doc \
libmaven-site-plugin-java libmaven-source-plugin-java \
libmaven-verifier-java libmaven-verifier-java-doc \
libmaven-war-plugin-java libmaven3-core-java \
libminify-maven-plugin-java libmodello-maven-plugin-java \
libmunge-maven-plugin-java libparanamer-maven-plugin-java \
libpolyglot-maven-java libpolyglot-maven-java-doc \
libproperties-maven-plugin-java libsisu-maven-plugin-java \
libstring-template-maven-plugin-java libxml-maven-plugin-java \
libxmlbeans-maven-plugin-java maven maven-ant-helper \
maven-cache-cleanup maven-debian-helper maven-repo-helper \
ruby-maven-libs libjax-maven-plugin libjaxb2-maven-plugin-java 

```



## Como usar:

### Instale os POMs primários e os arquétipos

1.  Clone este repositório.

2. Instale as bibliotecas (pacotes jars) no repositório local do maven

```bash
cd br.com.miguelpenteado.execucao.principal/  && mvn clean &&  mvn install && cd ../
cd br.com.miguelpenteado.execucao.estatica/   && mvn clean &&  mvn install && cd ../
cd br.com.miguelpenteado.execucao.executavel/ && mvn clean &&  mvn install && cd ../
cd br.com.miguelpenteado.projeto.estatica/    && mvn clean &&  mvn install && cd ../
cd br.com.miguelpenteado.projeto.executavel/  && mvn clean &&  mvn install && cd ../
ls
mkdir -p construcao/executavel
mkdir -p construcao/biblioteca
```

### Criar um projeto executável usando o arquetipo executável e execute
o arquivo executável.

1. Gerando um projeto com o arquétipo 
`br.com.miguelpenteado.projeto.executavel` que você instalou na 
máquina local. Dê o nome de **OlaMundo** ao seu projeto e empacote-o
dentro do pacote **br.com.miguelpenteado.aplicacao**

```bash
cd construcao/executavel
mvn archetype:generate \
	-DarchetypeGroupId=br.com.miguelpenteado.projeto \
	-DarchetypeArtifactId=executavel \
	-DarchetypeVersion=0.0.1 \
	-DgroupId=br.com.miguelpenteado.aplicacao \
	-DartifactId=OlaMundo \
	-Dversion=0.0.1
```
2. Entre no diretório gerado OlaMundo e compile o projeto
```bash
cd OlaMundo
mvn compile
```

3. Execute o executável **OlaMundo.uexe**
```bash
./target/OlaMundo.uexe
```

Parabéns! Você executou o seu primeiro programa binário que foi 
compilado com o Native Maven Plugin !

### Criar um projeto de biblioteca estática usando o arquetipo
de biblioteca estática.


1. Gerando um projeto com o arquétipo 
`br.com.miguelpenteado.projeto.estatica` que você instalou na 
máquina local. Dê o nome de **libMinhaBiblioteca** ao seu projeto e 
empacote-o dentro do pacote **br.com.miguelpenteado.biblioteca**

```bash
mvn archetype:generate \
	-DarchetypeGroupId=br.com.miguelpenteado.projeto \
	-DarchetypeArtifactId=estatica \
	-DarchetypeVersion=0.0.1 \
	-DgroupId=br.com.miguelpenteado.biblioteca \
	-DartifactId=libMinhaBiblioteca \
	-Dversion=0.0.1
```
2. Entre no diretório gerado libMinhaBiblioteca e compile o projeto
```bash
cd libMinhaBiblioteca
mvn compile
```

3. Veja a bibloteca gerada **libMinhaBiblioteca.a**
```bash
tree -P libMinhaBiblioteca.a
```


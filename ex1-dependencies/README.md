# Descrição do que fazer

1. Criar 3 projetos maven simples com as configurações mínimas conforme visto acima.

    ```xml
        <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                            http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>br.com.treinamento</groupId>
        <artifactId>nome-seu-projeto</artifactId>
        <version>1.0.0</version>
        </project>
    ```

   - Vamos organizar na estrutura:

        projeto-ex01

            Projeto 01 dentro da pasta projeto-ex01 do tipo jar

        projeto-ex02

            Projeto 02 dentro da pasta projeto-ex02 do tipo jar

        projeto-ex03

            Projeto 03 dentro da pasta projeto-ex03 do tipo war

   - Cada pasta vai possui apenas o arquivo pom.xml com a configuração mínima para um projeto Maven funcionar corretamente.
   
<hr/>

2. Executar o comando de empacotaemnto do Maven.

   - Acessar a pasta do projeto-ex01 e executar o comando abaixo para compilar e gerar o pacote do nosso projeto.
        ```java
            mvn package
        ```
    - Repetir o comando para os projetos projeto-ex02 e projeto-ex03 e verificar o resultado.
    
<hr/>

3. Ajustar configuração do projeto-ex03.

    - Neste ponto você deve ter percebido que o projeto-ex03 não executou corretamente, para corrigir esse problema neste momento vamos configurar para ignorar a falta do arquivo web.xml pois não é o foco neste momento.Propriedades "Dependencies"

    - Acessar e editar o arquivo pom.xml com a configuração abaixo:

        ```xml
        <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                            http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>br.com.treinamento</groupId>
        <artifactId>projeto-ex03</artifactId>
        <version>1.0.0</version>
        <packaging>war</packaging>

        <build> 
            <plugins>
            <plugin> 
                <artifactId>maven-war-plugin</artifactId>
                <version>3.1.0</version>
                <configuration>
                <failOnMissingWebXml>false</failOnMissingWebXml> 
                </configuration>
            </plugin>
            </plugins>
        </build>

        </project>
        ```


    - Executar novamente o build e verificar o resultado de sucesso!

<hr/>

4. Adicionando dependência entre os projetos.
    - Adicionar como dependência no pom.xml do <b>projeto-ex02</b> o <b>projeto-ex01</b> e executar o comando de empacotamento do maven.


    - Ao executar o comando para gerar o artefado do projeto-ex02 o Maven verifica que é necessário obter o artefato do projeto-ex01 para continuar com o processo de build. Como o ele não encontra no repositório de artefatos remoto o build falha.

    - Como já visto o Mavem tem um repositório local de artefatos pra fazer o cache e não baixar sempre que um comando de build for executado. Vamos colocar nosso projeto-ex01 nesse repositório local para resolver o problema.

    - Executar o comando de instalção local para resolver o problema.
    
    ```java
        mvn install
    ```


    Veja que temos o resultado de sucesso.
<hr/>

5. Adicionar dependência ao projeto-ex03

    - Adicionar como dependência no <b>projeto-ex03</b> o <b>projeto-ex02</b>

    - Executar o comando de empacotamento no <b>projeto-ex03</b>

        - Verificar a pasta projeto-ex03/target/projeto-ex03-1.0.0/WEB-INF/libs e veja os 2 artefatos copiados lá.
<hr/>

6. Configurar exclusão de dependência transitiva no projeto-ex03
   - Adicionar um exclusion para o projeto-ex01 na dependência projeto-ex02

        ```xml
        <dependency>
          <groupId>br.com.treinamento</groupId>
          <artifactId>projeto-ex02</artifactId>
          <version>1.0.0</version>
          <exclusions>
            <exclusion>
              <groupId>br.com.treinamento</groupId>
              <artifactId>projeto-ex01</artifactId>
            </exclusion>
          </exclusions>
        </dependency>
        ```

    - Executar o comando de empacotamento no projeto-ex03 mais antes apagar a pasta target com o comando mvn clean

    - Verificar a pasta projeto-ex03/target/projeto-ex03-1.0.0/WEB-INF/libs devemos ter somtente 1 artefato agora.

    ### **Este é o básico de adicionar dependências em um projeto.**


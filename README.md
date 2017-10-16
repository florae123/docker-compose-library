# Library Application

For more information about the application see: [https://github.com/florae123/LibraryApp-user](https://github.com/florae123/LibraryApp-user).

## Prerequisites

  The software needed for the following steps:
  * Docker
  * Docker Compose
  * Minikube
  * Git tool ([Download here](https://git-scm.com/downloads))

## Deploy using Docker Compose

1. Create an an instance of each of the following services on Bluemix:
    * Watson Conversation
    * Watson Text-To-Speech
    * App ID

    Copy the credentials of these services into the file **node-variables.env**:
    * *CONVERSATION_USERNAME*, *CONVERSATION_PASSWORD* from the Conversation Service credentials; *conv_workspaceid* should be the ID of the workspace you are using; import the workspace from the file **Libraryui/conversation-workspace-user-adjusted.json**.
    * *tts_password*, *tts_username* from the TextToSpeech Service
    * *CLIENT_ID*, *OAUTH_SERVER_URL*, *SECRET*, *TENANT_ID* from the App ID service

2. If you want to use the CloudantNoSQL DB Service on Bluemix, set **CLOUDANT_DEVELOPER** to anything other than **1** in the file **db-variables**. Also, set the variables **username** and **password** to the username and password from the Cloudant Service credentials.

    Otherwise, **CLOUDANT_DEVELOPER** should be set to **1**.

3. Build and run all docker containers:
    ```
    docker-compose up
    ```

4. Open the user interface for the libraryapp running on **http://localhost:8080/**.


## Deploy on Minikube

1. Start Minikube if necessary:
    ```
    minikube start
    ```

2. If you are using Docker Quickstart Terminal on Windows, execute this command:
    ```
    $ eval $(minikube docker-env)
    ```

3. Make sure kubectl interacts with the Minikube cluster.
    ```
    kubectl config use-context minikube
    ```
    Verify that kubectl is configured to communicate with your cluster:
    ```
    kubectl cluster-info
    ```

4. Navigate into the repository "docker-compose-library" and build the necessary Docker Images:
    * the Java server image:
      ```
      docker build -t library-server:v1 ./library-server-java
      ```
    * the Node.js server and frontend image:
      ```
      docker build -t library-ui:v1 ./Libraryui
      ```
5. * If you want to use the CloudantNoSQL DB service on Bluemix, make sure the environment variable **CLOUDANT_DEVELOPER** in the file **library-server.yaml** is set to anything other than "1", and copy the username and password of the CloudantNoSQL service credentials to the variables **username** and **password**.
   * If you do not want to use the CloudantNoSQL DB service on Bluemix, but an instance of Cloudant running in a container, set the environment variable **CLOUDANT_DEVELOPER** in the file **library-server-yaml** to "1".

     Create a deployment and a service for the database:
       ```
       kubectl create -f cloudant-developer.yaml
       ```
   * Open the dashboard for the Database, either by clicking **Launch** if your Service is running on Bluemix, or with:
    ```
    minikube service cloudant-developer
    ```
      If the latter, add **/dashboard.html** to the URL and enter the username **admin** and the password **pass**.

      Configure the databases as described in [https://github.com/florae123/library-server-java-v2#configure-databases](https://github.com/florae123/library-server-java-v2#configure-databases)

6. You should have created an instance of each of the following services on Bluemix:
    * Watson Conversation
    * Watson Text-To-Speech
    * App ID

    Copy the credentials of these services into the file **libraryui.yaml**:
    * *CONVERSATION_USERNAME*, *CONVERSATION_PASSWORD* from the Conversation Service credentials; *conv_workspaceid* should be the ID of the workspace you are using; import the workspace from the file **Libraryui/conversation-workspace-user-adjusted.json**.
    * *tts_password*, *tts_username* from the TextToSpeech Service
    * *CLIENT_ID*, *OAUTH_SERVER_URL*, *SECRET*, *TENANT_ID* from the App ID service

7. Check for the external IP address that minikube uses to expose services. Copy the IP address to the values of the environment variables **LIBRARY_URI** and **APP_URL**. Keep the ports *30190* and *30832*, respectively, and the rest of the URLs.

8. Create a deployment and a service for the to microservices.
    First, deploy and expose the library-server app.
    ```
    kubectl create -f library-server.yaml
    ```
    Then, deploy and expose the library-ui app.
    ```
    kubectl create -f libraryui.yaml
    ```

9. Open the application frontend

    ```
    minikube service library-ui
    ```
    and log in with your google or facebook account.

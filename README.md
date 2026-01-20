# OIDC-Demo-showcase-by-Viktor-Larsson

Step by step guide for setting up and running workspace:

1. You'll need docker running. When you have docker running you can run the following command to setup your docker container,
this will be our workspace. Just replace the area {REPLACE WITH FOLDER} with the folder link to this directory and then run the line below inside powershell:
docker run -p 127.0.0.1:8080:8080 -e KC_BOOTSTRAP_ADMIN_USERNAME=admin -e KC_BOOTSTRAP_ADMIN_PASSWORD=admin -v {REPLACE WITH FOLDER DIRECTORY}\keycloak:/opt/keycloak/data/import quay.io/keycloak/keycloak:26.5.1 start-dev --import-realm

2. Now we need to set our client_secret. find container name under docker ps and use it in every {CONTAINER_NAME} placement. I.e replace {CONTAINER_NAME} with the appropriate container name.

run in powershell:
docker ps
docker exec -it {CONTAINER_NAME}
"/opt/keycloak/bin/kcadm.sh config credentials \
   --server http://localhost:8080 \
   --realm master \
   --user admin \
   --password admin" (COPY ONLY THE CODE INSIDE THE QUOTATION MARKS)
/opt/keycloak/bin/kcadm.sh get clients -r testrealm --query clientId=testclient

run in cmd:
docker exec {CONTAINER_NAME} /opt/keycloak/bin/kcadm.sh update clients/c9cada7b-3358-4141-afd8-86236b0c1b65 -r testrealm -s secret=tFI5wKIPbAF4RHYq0sryhsymSt8kLD8D

3. Dependencies, you need python installed to run this command, but running the command will install the required
libraries for this workspace:
pip install -r requirements.txt

4. To run the program, open cmd and cd (change directory) into this folder location. Then run
python app.py

Now everything should be running.
The ADMIN UI is on http://localhost:8080
And the app url is https://localhost:8000
Try opening them up in your browser.

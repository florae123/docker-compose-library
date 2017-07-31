FROM node:latest

RUN mkdir -p /app
# Set the working directory to /app
WORKDIR /app

# Install app dependencies
COPY package.json /app/
RUN npm install

# Copy the current directory contents into the container at /app
ADD . /app

EXPOSE 8080

ENV LIBRARY_URI=http://169.46.22.188:9080/library-server-java/api
ENV CONVERSATION_USERNAME=1e642087-a24b-4277-b021-0ff372845a5e
ENV CONVERSATION_PASSWORD=7F7MvTfwPuTt
ENV conv_workspaceid=4e3c0199-9871-4346-8b30-c2bfba973f8c
ENV tts_username=aa348980-c0d8-4c7a-87ae-ac2c77fb9d25
ENV tts_password=JqtrtmFEqG26
ENV inContainer=1
# credentials for app id service
ENV TENANT_ID=21800a63-541d-47dd-8774-34f0d6c063f3
ENV CLIENT_ID=68ada283-cea7-470d-ab8c-21571d080eeb
ENV SECRET=ODg3YjcyNzAtYTgxMy00M2MwLTgyZDEtM2UxNGY1ODBhYWZj
ENV OAUTH_SERVER_URL=https://appid-oauth.ng.bluemix.net/oauth/v3/21800a63-541d-47dd-8774-34f0d6c063f3
ENV APP_URL=http://localhost:8080


CMD [ "npm", "start" ]

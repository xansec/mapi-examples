FROM node:14

# Typescript plugin

WORKDIR /app
COPY . ./
RUN npm install
RUN npx tsc
RUN node /app/dist/plugin.js &

#EXPOSE 50051

# Download and run Mayhem

WORKDIR /mayhem
ARG MAYHEM_TOKEN
RUN curl --fail -L https://app.mayhem.security/cli/Linux/install.sh | sh
RUN /mayhem/mapi --mayhem-url https://app.mayhem.security login $MAYHEM_TOKEN

RUN /mayhem/mapi run petstore/api 30 'https://demo-api.mayhem.security/api/v3/openapi.json' --url 'https://demo-api.mayhem.security/api/v3/' --header 'Content-Type: application/json' --header-auth 'api-key: special-key' --rewrite-plugin http://localhost:50051
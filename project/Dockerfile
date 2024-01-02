FROM node:alpine3.15 AS build
COPY ./flask-app ./flask-app
#npm install
RUN apk add npm
WORKDIR /flask-app
RUN npm install && npm run build 

FROM alpine:3.15
COPY --from=build /flask-app ./flask-app/
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache python2 && \
     python2 -m ensurepip  && \
     pip install --no-cache --upgrade pip setuptools
RUN pip install -r flask-app/requirements.txt
ENTRYPOINT ["python2", "app.py"]

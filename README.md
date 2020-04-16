# Cloud-psql-client-using-the-Cloud-SQL-Proxy-docker-Image
This explain how to connect google cloud postgres database using proxy docker image which is provided by google

>Link to documentation
https://cloud.google.com/sql/docs/postgres/connect-docker

>Start downloaded docker image
```
docker run -it \
  -v /home/ghost/Sameera/CloudPosgres:/config \
  -p 127.0.0.10:5432:5432 \
  gcr.io/cloudsql-docker/gce-proxy:1.16 /cloud_sql_proxy \
  -instances=buzzbetatest:us-central1:buzzflow-beta=tcp:0.0.0.0:5432 -credential_file=/config/buzzbetatest-20fda0b6f804.json
```

> Following cmd also worked without ip mapping.
```
docker run -it \
  -v /home/ghost/Sameera/CloudPosgres:/config \
  gcr.io/cloudsql-docker/gce-proxy:1.16 /cloud_sql_proxy \
  -instances=buzzbetatest:us-central1:buzzflow-beta=tcp:0.0.0.0:5432 -credential_file=/config/buzzbetatest-20fda0b6f804.json
```

>Then have to identify ip address by running
```
 $ docker inspect -f '{{ .NetworkSettings.IPAddress }}' <container_id>
```

>Note: Use -d instanced of -it, for run background


>Start the client:
```
  psql "host=127.0.0.1 sslmode=disable dbname=<DB_NAME> user=<USER_NAME>"
```
>Could change ip address instead of 127.0.0.1

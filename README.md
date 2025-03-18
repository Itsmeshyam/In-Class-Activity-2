# In-Class-Activity-2
 In-Class Activity-2 (Graded)
 This in-class activity will assess your understanding on containerized application deployed into a Kubernetes Cluster. You will deploy a Wordpress stack along with a Proxy sever in a Kubernetes cluster. So, there will be 3 components you will deploy as part of this stack:

1) An nginx reverse proxy
2) A Wordpress application
3) A mariaDB database

For each component, you will create required Kubernetes resoruces to work them together. The flow is: Internet -> Nginx-proxy -> Wordpress app -> Database. You may use a local Kubernetes cluster or a cluster in any Cloud provider. Remember that the database should be deployed as a container as well.

Follow the instruction to complete this activity:

- Each component must be deployed into it's own namespace - say proxy, wp, db
- You will expose Nginx proxy to external only. Use any port of your choice. Rest of them (Wordpress and Database) should NOT be exposed to public

- For nginx-proxy: 
- Create a Dockerfile and use the following config to pass traffic to Wordpress component. Use any base image of your choice.
server {
  listen 80;
  location / {
    proxy_pass http://<your-upstream-url>:<upstream-port>;
    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Forwarded-Port $server_port;
    proxy_set_header X-Forwarded-Host $host;
  }
}
- For Wordpress: 
- Use wordpress:latest image and set the following env variables:
WORDPRESS_DB_HOST
WORDPRESS_DB_USER
WORDPRESS_DB_PASSWORD
WORDPRESS_DB_NAME
- Container port is 80 and create 3 pods
- Use the following labels for the pods and use id as selector 
id: <your-college-id>
app: wp-app
env: dev

- For Database:
- Use mariadb:10.6.4-focal image and set the following env variables:
MYSQL_ROOT_PASS
WORDMYSQL_DATABASE
MYSQL_USER
MYSQL_PASSWORD
- Container port is 3306 and create 3 pods
- Use the following labels for the pods and use id as selector 
id: <your-college-id>
app: db
env: dev
- Create required K8s manifests for each component (nginx-proxy, wordpress app and database) and use them to deploy into your K8s cluster

- Make sure you use proper labeling as mentioned above
- Organize the manifests, Dockerfiles, etc. into 3 different folders by their component name - say proxy, wp, db
- Create a GitHub repository and upload all the files into the repository
- Better if you don't use minikube or docker desktop based k8s cluster


Deliverables:
- Push all manifest to a git repository
- Properly configured all three components and a working stack

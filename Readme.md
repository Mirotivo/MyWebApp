dotnet new web -n MyWebApp
cd MyWebApp

***********************************************

docker build -t my-web-app .
docker run -d -p 80:80 --name my-web-app-container my-web-app

***********************************************

aws ecr create-repository --repository-name my-web-app
aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.<your-region>.amazonaws.com
docker tag my-web-app <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/my-web-app
docker push <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/my-web-app

aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.<your-region>.amazonaws.com
docker pull <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/my-web-app
docker run -d -p 80:80 <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/my-web-app

***********************************************

aws ecr create-repository --repository-name my-web-app
docker tag my-web-app <registry-url>/my-web-app
docker push <registry-url>/my-web-app

docker pull <registry-url>/my-web-app
docker run -d -p 80:80 <registry-url>/my-web-app

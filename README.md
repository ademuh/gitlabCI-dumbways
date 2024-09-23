# GitlabCI
https://gitlab.com/ademuh

## Requirements
1. Gitlab Account (Using SaaS)
2. CI/CD Server with Gitlab-runner installed (on top docker/native)
3. Dumbflix/Wayshub application on repository

## Gitlab vs Jenkins
| Gitlab   | Jenkins |
|----------|---------|
| CI/CD without any installations | powerful CI/CD with a lot of plugins |
| All-in-one SCM (deployments, pipeline etc) | - |
| Hosted by Gitlab, Gitlab Runner to use own servers | Hosted internally, Preferred by devs |
| Free, Self-Managed | Open Source |

**Gitlab** is a strong tool for _Version Control_ and _Code Collaborations_ while **Jenkins** is ideal for _Continuous Integration_ with a lot of plugins to use.

## Step-by-step : First Setup
1. Register a Gitlab Account
2. Create a new repository
![image](https://user-images.githubusercontent.com/111945026/220281073-c4967bf2-b9f6-4752-8757-800a224cd508.png)

3. Create a blank project
![image](https://user-images.githubusercontent.com/111945026/220281348-4cabc40a-ac1d-490e-ad9d-f2ab8d3f5eb4.png)

4. Setup a **SSH Key** for Gitlab access

```
User Settings > SSH Keys
```
![image](https://user-images.githubusercontent.com/111945026/220283347-9f880f65-8688-4e05-8a23-3773b8e8cf4b.png)

5. Setup Gitlab Runner
Create a VM with any _Cloud Computing Providers_, and then install gitlab-runner

Binary install :
```
curl -LJO "https://gitlab-runner-downloads.s3.amazonaws.com/latest/deb/gitlab-runner_${arch}.deb"

dpkg -i gitlab-runner_<arch>.deb
```

Docker Container :
```
docker volume create gitlab-runner-config

docker run -d --name gitlab-runner --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v gitlab-runner-config:/etc/gitlab-runner \
    gitlab/gitlab-runner:latest
```

After installation, connect the runner into the repository
```
Repository Settings > CI/CD
```
![image](https://user-images.githubusercontent.com/111945026/220284498-bb935343-d013-438b-9657-ba8dd926d86c.png)

6. From here, we can clone the `Dumbflix/Wayshub` repository into the Gitlab Project
```
git clone https://github.com/dumbwaysdev/dumbflix-frontend

ssh git@gitlab.com

git remote origin set-url git@gitlab.com:<gitlab-user>/<project-name>.git

git push origin <branch>

```

## Step-by-step : Pipeline
1. Go to `CI/CD > Pipeline`
2. We can use a template pipeline or create a new one
![image](https://user-images.githubusercontent.com/111945026/220286467-2ac82af4-fd79-422c-adb9-b07be7bbb2a1.png)

3. A new file will be created (`.gitlab-ci.yml`), we can modify it as we see fit (example available in this repository)
![image](https://user-images.githubusercontent.com/111945026/220287111-ab0596a3-db30-48c8-bb4a-255dac140d00.png)

4. Gitlab repository changes will trigger the pipeline automatically
![image](https://user-images.githubusercontent.com/111945026/220287332-0a7ccae7-1dd2-45ba-8921-948c1c798fed.png)



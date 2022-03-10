# Lightdock
Light PHP development environment based on Docker.

---

### How to use

1 - Clone the repository:
```
git clone git@github.com:np4p/lightdock.git
```

2 - Copy the `.env.example` file to `.env`
```
cp lightdock/.env.example lightdock/.env
```

3 - Run docker-compose up -d
```
cd lightdock
docker-compose up -d
```

4 - Created default project
```
cd ../code
mkdir default/public
cp ../lightdock/index.php default/public/index.php
```

5 - Visit http://localhost

---
If you have any questions, welcome to issue.

# Dockerfiles for CakePHP 4.x Installation 🥧

Basic docker configuration to setup ready to use CakePHP 4.x project.

Choose prefered local URL to use editing `dockerfiles/nginx/site.template` (now we have babba.local)

```sh

git clone https://github.com/RoBYCoNTe/friendsofbabba-dockerfiles.git myapp
cd myapp/dockerfiles
docker compose up -d
docker exec -it babba_php bash
cd /var/www/html
./install.sh
```

## Tips

This configuration contains xDebug ready to use configuration.

# Dockerfiles for CakePHP 4.x Installation

This is a basic docker configuration necessary to work with CakePHP 4.x project.
To create your new CakePHP 4.x project:

```sh

git clone https://github.com/RoBYCoNTe/friendsofbabba-dockerfiles.git myapp
cd myapp
docker compose up -d
docker exec -it babba_php bash
composer create-project --prefer-dist cakephp/app:~4.0 .
```

## Tips

This configuration contains xDebug ready to use configuration.

### Пример подключения веб-интерфейса на mongo-express к базе данных Mongo с использованием контейнеров Docker
Для запуска в отдельных контейнерах (веб интерфейс будет на http://localhost:8081/)

1 создаем сеть
```dockerfile
docker network create web_default
```
2 запускаем монго
```dockerfile
docker run --rm -d -p 27017:27017 --network web_default --name mongo mongo
```
3 запускаем монго-экспресс без авторизации в вебе
```dockerfile
docker run -it --rm --name mongo-express --network web_default -p 8081:8081 -e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" -e ME_CONFIG_BASICAUTH_USERNAME="" -e ME_CONFIG_MONGODB_URL="mongodb://mongo:27017" mongo-express
```
или с авторизацией
```dockerfile
docker run -it --rm --name mongo-express --network web_default -p 8081:8081 -e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" -e ME_CONFIG_BASICAUTH_USERNAME="black1277" -e ME_CONFIG_BASICAUTH_PASS
WORD="superpass" -e ME_CONFIG_MONGODB_URL="mongodb://mongo:27017" mongo-express
```
=======================================================================

Для запуска в композе
```dockerfile
docker-compose up -d
```
Остановка
```dockerfile
docker-compose down
```
Для очистки системы:
 - удалить все тома принудительно
```dockerfile
docker volume prune -f 
```
 - удалить созданную сеть
 ```dockerfile
docker network rm web_default
```

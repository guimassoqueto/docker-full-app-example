0. docker network create node_app --driver bridge
1. docker run --name mongodb -e MONGO_INITDB_ROOT_USERNAME=user -e MONGO_INITDB_ROOT_PASSWORD=password -v data:/data/db --rm --network node_app -d mongo
2. docker build -t goals-node backend/
3. docker run --name goals-backend -v $(pwd)/backend:/app -v /app/node_modules --rm --network node_app -d -p 8000:8000 goals-node
4. docker build -t goals-react frontend/
5. docker run --name goals-frontend -v $(pwd)/frontend/src:/app/src --rm -it -p 3000:3000 goals-react
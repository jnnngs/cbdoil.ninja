docker image build --no-cache -t gilsteadprivatehire .

docker tag gilsteadprivatehire:latest reg.jnnn.gs/gilsteadprivatehire:latest

docker login reg.jnnn.gs

docker push reg.jnnn.gs/gilsteadprivatehire:latest

docker run --rm --name gilsteadprivatehire --pull=always -p 30080:80 --hostname gilsteadprivatehire -d reg.jnnn.gs/gilsteadprivatehire:latest

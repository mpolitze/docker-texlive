
docker run --rm -p5000:5000 -d --name registry registry:2

docker buildx build -f Dockerfile.simple --load --platform linux/amd64 --tag localhost:5000/tmp:amd64 .
docker buildx build -f Dockerfile.simple --load --platform linux/arm64 --tag localhost:5000/tmp:arm64 .

docker push localhost:5000/tmp:amd64
docker push localhost:5000/tmp:arm64

docker buildx imagetools create --tag ghcr.io/mpolitze/docker-texlive:latest localhost:5000/tmp:arm64 localhost:5000/tmp:amd64
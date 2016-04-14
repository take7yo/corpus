```
# 查看docker信息
docker info
docker_sample_job=$(docker run -d ubuntu /bin/sh -c "while true; do echo Docker; sleep 1; done")
docker logs $docker_sample_job
docker help
docker stop $docker_sample_job
docker restart $docker_sample_job
docker rm -f $docker_sample_job
## 镜像名称只能取字符[a-z]和数字[0-9]
docker commit $docker_sample_job job1
docker images
docker search (image-name)
docker history (image-name)
docker push (image-name)
```
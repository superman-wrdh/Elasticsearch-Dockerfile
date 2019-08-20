## **[English](README.md)** **[简体中文](README_ZH.md)**
# Dockerfiles

## 关于这个仓库

这个仓库是基于官方Elasticsearch镜像,构建包含了elasticsearch-analysis-ik 分词器的 Elasticsearch镜像,并使用docker-compose添加了Kibana工具
在相应的版本下目录下执行
```bash
# docker build -t elasticsearch_images_name:version_tag .  # 可以修改elasticsearch_images_name:version_tag成自己定义的名字
```
构建成功后,修改 docker-compose.yml文件
```yaml
version: "2.1"
services:
  myelasticsearch:
    image: elasticsearch_images_name:version_tag # 将这里修改成上面build时候的名字
    volumes:
      - ~/myesdata:/usr/share/elasticsearch/data
    ports:
      - "9200:9200"
      - "9300:9300"
    networks:
      - docker_elk
  kibana:
    image: kibana:version_tag  # 注意这里的版本要和上面elasticsearch版本一致
    ports:
      - "5601:5601"
    links:
      - elasticsearch
    networks:
      - docker_elk
networks:
  docker_elk:
    driver: bridge
```

然后执行 docker-compose up  
或者 docker-compose up -d # 后台守护模式运行
之后浏览器访问 http://you_host:9200 输出es版本信息启动成功
http://you_host:5601 进入kibana
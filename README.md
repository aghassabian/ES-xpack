# Elasticsearch with X-Pack
Elasticsearch 5.5 with x-pack plugin installed.

# Run by Command
To run directly on host using ```docker run``` command, should set both the JVM memory allocation and exposed ports using the following command:
```bash
docker run -itd --name elasticsearch -p 9200:9200 -p 9300:9300 -e "ES_JAVA_OPT=-Xms512m -Xmx1g" aghassabian/es-xpack
```
The size of allocated memory to JVM is depend on your usage and system specification.

# run using Ansible
To run using Ansible add the following section to ansible role or playbook:
```yaml

- name: Run Elasticsearch
  docker_container:
    name: elasticsearch
    image: aghassabian/es-xpack
    state: started
    networks:
      - name: "{{ elastic_network }}"
    ports:
      - "9200:9200"
      - "9300:9300"
    env:
        ES_JAVA_OPTS: "-Xms512m -Xmx1g"
```
elastic network should have already been created.

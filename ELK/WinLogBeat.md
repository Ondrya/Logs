# Сбор Windows Event Logs

Сбор логов Windows настраивается достаточно просто: 
   -   https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-installation-configuration.html
Важно помнить, что собираются текущие логи. То есть если надо загрузить уже существующие, то процесс несколько усложнится, но надо следовать этой инструкции:
   -   https://www.elastic.co/guide/en/beats/winlogbeat/current/reading-from-evtx.html

пример файла дополнительной конфигурации и его применения


## winlogbeat-evtx.yml

```yaml
winlogbeat.event_logs:
  - name: ${EVTX_FILE} 
    no_more_events: stop 

winlogbeat.shutdown_timeout: 30s 
winlogbeat.registry_file: evtx-registry.yml 

output.elasticsearch.hosts: ["10.16.6.216:9200"]

# для загрузки старых журналов надо выполнить команду
# .\winlogbeat.exe -e -c .\winlogbeat-evtx.yml -E EVTX_FILE=c:\backup\Security-2019.01.evtx
# где EVTX_FILE= - путь к архивному файлу журнала
# C:\windows\system32\winevt\Logs
# .\winlogbeat.exe -e -c .\winlogbeat-evtx.yml -E EVTX_FILE=C:\windows\system32\winevt\Logs\[filename]
```

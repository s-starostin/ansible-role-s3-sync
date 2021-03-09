ansible-role-s3-sync
=========

Роль для установки aws cli и создания cron-задачи для синхронизации директории на локальном хосте с S3-хранилищем.

Переменные
------------

| Variable | Type | Default | Comment |
| ------ | ------ | -------  | ---------- |
| s3_sync_aws_region | string | ru-central1 | Регион доступности для S3-хранилища (ru-central1 для YC) |
| s3_sync_aws_access_key_id | string | | Идентификатор ключа |
| s3_sync_aws_secret_access_key | string | | Секретный ключ |
| s3_sync_bucket | string | atlassian | Имя бакета для инхронизации |
| s3_sync_folder | string | /temp | Целевая директория в облаке |
| s3_sync_source_location | string | /root/tmp | Локальная директория синхронизации |
| s3_sync_endpoint_url | string | https://storage.yandexcloud.net | URL сервиса AWS |
| s3_sync_timer_calendar | string | *:0/10 | Период запуска синхронизации |

Пример плэйбука
--------------

    - hosts: nfs
      remote_user: superuser
      become: yes
      vars:
        - s3_sync_aws_access_key_id: 00000000000000000
        - s3_sync_aws_secret_access_key: 00000000000_000000000000000
        - s3_sync_bucket: dtcrt-atlassian
        - s3_sync_source_location: /root/share
      roles:
        - ansible-role-s3-sync
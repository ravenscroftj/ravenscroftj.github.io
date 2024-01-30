---
created: 2024-01-30T13:17
updated: 2024-01-30T13:17
title: Using Airflow with Google Cloud
---
Install [[Public/Software/Airflow/index|Airflow]] with `google` optional module: `pip install apache-airflow[google]`.

Credenials can be side-loaded in via an environment variable

`export AIRFLOW_CONN_GOOGLE_CLOUD_DEFAULT='{"conn_type": "google-cloud-platform", "key_path": "/secrets/key.json", "scope": "https://www.googleapis.com/auth/cloud-platform", "project": "airflow", "num_retries": 5}'`
#### Google OIDC auth 

It's possible to authenticate airflow against your google org using SAML/OpenID flow: https://airflow.apache.org/docs/apache-airflow-providers-google/stable/api-auth-backend/google-openid.html

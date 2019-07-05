
Install a python tool called httpie or use curl

```

http -v POST :8081/subjects/krish-file-content-value/versions \
  Accept:application/vnd.schemaregistry.v1+json \
  schema="{\"type\": \"string\"}"

```
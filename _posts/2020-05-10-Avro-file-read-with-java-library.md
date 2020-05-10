---
title: "Avro format read with java library `apache.avro`"
date: 2020-05-10 12:57:00
category: ["Back-end","Data Engineering"]
tag: ["apache.avro",
        "Java", "library"]
---

1)  Import ‘org.apache.avro:avro:1.9.0’ (choose proper version)
2)  follow like this

```java

    String path = getClass().getResource(path).getPath();
    File file = New File(path);

    DatumReader<GenericRecord> datumReader = new GenericDatumReader<>();
    DataFileReader<GenericRecord> dataFileReader = new DataFileReader<>(file, datumReader);
    record = dataFileReader.next(record);
    record.get(key).toString();
```


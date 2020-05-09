---
title: "How to Use FastText4J Library"
date: 2020-05-09 18:51:00
category: ["Back-end","Data Engineering"]
tag: ["FastText4J",
        "Java", "library"]
---

1)  Save fastest model bin file to AWS S3
    
2)  Import FastText4J library to Spring java project
    
    ```java
    dependency "com.github.linkfluence:fastText4j:0.2.1"
    compile('com.github.linkfluence:fastText4j')
    ```

3)  get fasttext model bin file from S3(Use AWS aws-java-sdk-s3 library)
    
4)  load FastText class with model bin
    
    ```java
    InputStream modelBinary;
    
    FastText fastText = FastText.loadModel(modelBinary);
    
    ```

5)  call predict function to get Prediction information

    ```java
    FastTextPrediction predictionInfo = fastText.predict(rawString);
    
    ```
[URL](https://velog.io/@dntjd7701/java.util.Properties)

### 키와 값으로 이루어진 properties 파일 읽고 작성하기 


> properties 파일 작성 

```java 
 private static void writeProps () {
        Properties prop = new Properties();
        prop.setProperty("SERVER_IP", "127.0.0.1");
        prop.setProperty("SERVER_PORT", "5000");
        try {
            OutputStream stream = new FileOutputStream("testProperty");
            prop.store(stream, "SERVER INFO");
            stream.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
```

> properties 파일 읽기 

``` java
 private static void readProps () {
        Properties prop = new Properties();
        try {
            InputStream stream = new FileInputStream("testProperty");
            prop.load(stream);
            stream.close();

            System.out.println(prop.getProperty("SERVER_IP"));


        } catch (IOException e ){

        }
    }
```

> 결과


![](https://velog.velcdn.com/images/dntjd7701/post/1b7e2a82-7cdd-4541-beb6-884ba26bf314/image.png)



> xml 파일을 properties 파일로 사용하기 

- load(), store() =>>> loadFromXML(), storeToXML() 사용 


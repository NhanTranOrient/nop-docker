# nop-docker

Step 1: Clone source code tại https://github.com/nopSolutions/nopCommerce  
Step 2: Mở file docker-compose.yml, viết lại code trong file như sau:
```
version: "3.4"
services:
    nopcommerce_web:
        build: .
        container_name: nopcommerce
        ports:
            - "80:80"
        depends_on:
            - nopcommerce_database
    nopcommerce_database:
        image: "mcr.microsoft.com/mssql/server:2019-latest"
        container_name: nopcommerce_mssql_server
        ports:
            - "14330:1433"
        environment:
            SA_PASSWORD: "nopCommerce_db_password"
            ACCEPT_EULA: "Y"
            MSSQL_PID: "Express"

volumes:
  nopcommerce_data:
```
Step 3: Tắt VPN OSD (do restore package có thể sẽ bị chặn và không restore được), mở cmd tại thư mục chứa file docker-compose.yml, gõ lệnh sau:
```
docker compose up -d
```
Step 4: Mở browser truy cập http://localhost/  
Step 5: Điền các field như sau
![alt text](https://github.com/NhanTranOrient/nop-docker/blob/main/1.png)
Step 6: Sau khi setup docker image tự động stop => run lại image =>  truy cập http://localhost/

## Optional
Nếu có MSSQL Management Studio và muốn thực hiện query truy vấn, có thể connect tới Server thông qua:  
ServerName: localhost,14330  
Login: sa  
Password: nopCommerce_db_password

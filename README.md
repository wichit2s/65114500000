 65114500000
 Wichit Sombat
 email@ubu.ac.th

## สร้าง repository ชื่อ 65114500000 บน github


## นำเข้า 65114500000

    gh repo clone withit2s/65114500000
    cd 65114500000

## นำเข้า KhootClone

1. clone จาก wichit2s/KhootClone

    gh repo clone wichit2s/KhootClone

2. เปลี่ยนเป็น branch ชื่อ channels

    cd KhootClone/
    git checkout channels

3. ลบ .git

    rmdir .git

## ติดตั้ง Docker Desktop

 * https://docs.docker.com/desktop/

## ดึง image จาก https://hub.docker.com

    docker pull nginx:latest
    docker pull mysql:8.0
    docker pull python:3.11

## สร้างและเปิดใช้งาน container ชื่อ mysql4dj จาก image ชื่อ mysql รุ่น 8.0

    docker run --name mysql4dj -p 3306:3306 -d -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=dbuser -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=khootclonedb mysql:8.0

## รันคำสั่ง mysql -version บน container ชื่อ mysql4dj

    docker exec mysql4dj mysql -version

## เขียน Dockerfile

```yaml
FROM python:3.11

WORKDIR /khootclone

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN python manage.py makemigrations

RUN python manage.py migrate

EXPOSE 8000

CMD ["python", "manage.py", "runserver"]
```

## สร้าง image ชื่อ khootclone รุ่น 0.1.0

    docker build -t khootclone:0.1.0 .

## สร้างและเปิดใช้งาน container ชื่อ khootcloneapp จาก image ชื่อ khootclone รุ่น 0.1.0

    docker run --name khootcloneapp -p 80:8000 khootclone:0.1.0


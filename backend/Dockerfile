FROM openjdk:21-jdk-slim

# ตั้งค่า Working Directory เป็น /app
WORKDIR /app

# คัดลอกไฟล์โปรเจกต์ทั้งหมดจาก backend ไปยัง container
COPY . .

# แก้ปัญหา CRLF (Windows Line Endings) ในไฟล์ `mvnw`
RUN sed -i 's/\r$//' mvnw && chmod +x mvnw
RUN sed -i 's/\r$//' wait-for-it.sh && chmod +x wait-for-it.sh

RUN ./mvnw dependency:resolve

RUN ./mvnw package -DskipTests

CMD ["./wait-for-it.sh", "my-mysql:3306", "--", "java", "-jar", "target/transport-application-0.0.1-SNAPSHOT.jar"]